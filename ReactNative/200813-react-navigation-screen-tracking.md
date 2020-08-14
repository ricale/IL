# [React Native] React Navigation 에 Firebase Analysis 적용

#### Environment

- react-native 0.62
- @react-navigation/native 5.2.3
- @react-navigation/stack 5.2.18
- @react-navigation/bottom-tabs 5.7.0
- @react-native-firebase/app 8.3.0
- @react-native-firebase/analytics 7.4.1

#### References

- [React Navigation - Screen tracking for analytics][react-navigation-doc]
- [React Native Firebase - Analytics](https://rnfirebase.io/analytics/usage)

---

[React Navigation 의 공식 문서][react-navigation-doc]에서, 앱 사용자들이 어떤 화면에 접속하는지 (통계적인 용도로) 트래킹하기 위한 코드를 제공해준다.

```jsx
import * as React from 'react';
import * as Analytics from 'expo-firebase-analytics';
import { NavigationContainer } from '@react-navigation/native';

export default function App() {
  const routeNameRef = React.useRef();
  const navigationRef = React.useRef();

  return (
    <NavigationContainer
      ref={navigationRef}
      onReady={() => routeNameRef.current = navigationRef.current.getCurrentRoute().name}
      onStateChange={() => {
        const previousRouteName = routeNameRef.current;
        const currentRouteName = navigationRef.current.getCurrentRoute().name

        if (previousRouteName !== currentRouteName) {
          // The line below uses the expo-firebase-analytics tracker
          // https://docs.expo.io/versions/latest/sdk/firebase-analytics/
          // Change this line to use another Mobile analytics SDK
          Analytics.setCurrentScreen(currentRouteName);
        }

        // Save the current route name for later comparision
        routeNameRef.current = currentRouteName;
      }}
    >
      {/* ... */}
    </NavigationContainer>
  );
}
```

하지만 사용하려고 하니 잘 되지 않았다. 일단 `navigationRef.current.getCurrentRoute` 함수가 존재하질 않았다. 그리고 `NavigationContainer.onStateChange` 는 `state` 파라미터를 제공하는데, 이 코드에서는 그 파라미터를 활용하지 않는 것도 이상했다. 라이브러리 버전 문제인 건가 싶다가도, 문서에 'Version: 5.x'라고 명시되어 있는 걸 보면 아닌 것 같아 어안이 벙벙해진다. 여하튼 안 된다고 하지 않을 수는 없다. 월급은 받아야 하니까.

다른 방법을 찾아보자.

`onStateChange`의 `state` 파라미터는 아래와 같은 형식이다.

```tsx
export declare type NavigationState = {
    key: string; // Unique key for the navigation state.
    index: number; // Index of the currently focused route.
    routeNames: string[]; // List of valid route names as defined in the screen components.
    history?: unknown[]; // Alternative entries for history.
    routes: (Route<string> & {
        state?: NavigationState | PartialState<NavigationState>;
    })[]; // List of rendered routes.

    /**
     * Custom type for the state, whether it's for tab, stack, drawer etc.
     * During rehydration, the state will be discarded if type doesn't match with router type.
     * It can also be used to detect the type of the navigator we're dealing with.
     */
    type: string;
    /**
     * Whether the navigation state has been rehydrated.
     */
    stale: false;
};
```

내가 알고 싶은 것은 사용자의 현재 화면이다. 그래야 사용자가 어느 화면에 들어갔는지 트래킹이 가능하다.

위 타입 설명에 의하면 `state.routes[state.index]` 로 현재 화면을 찾을 수 있을 것 같다. 하지만 라우팅이 중첩된 경우에는 또다른 `state` 값이 들어있을 수 있다. 따라서 재귀적으로 들어가야 한다.

```tsx
type GetCurrentRouteResult = {
  name?: string
  params?: object
} | null

function getCurrentRoute(
  state: NavigationState | PartialState<NavigationState> | undefined
): GetCurrentRouteResult {

    if (!state) {
        return null; 
    }

    const route = state.routes[state?.index || 0];

    if (route.state) {
        return getCurrentRoute(route.state);
    }

    return {
        name: route?.name,
        params: route?.params,
    };
}
```

좋다. 그럼 이 함수를 `NavigationContainer.onStateChange`에서 써 보자. 

```tsx
const previousRouteRef = useRef<GetCurrentRouteResult>(null);
const onStateChange = useCallback((state: NavigationState | undefined) => {
    const previousRoute = previousRouteRef.current;
    const currentRoute = getCurrentRoute(state);

    if(previousRoute?.name !== currentRoute?.name) {
        analytics().setCurrentScreen(currentRoute?.name);
    }

    previousRouteRef.current = currentRoute;
}, []);
```

위에서 작성한 `getCurrentRoute` 함수를 통해 현재 화면에 관한 정보를 얻고, 이전 화면 정보 (`previousRouteRef.current`) 와 다르다면 firebase 의 `analytics` 에 기록한다.

잘 동작한다.

[react-navigation-doc]: https://reactnavigation.org/docs/screen-tracking/
