
# [React Native] React Navigation 

#### Environment

- react-native 0.62
- typescript 3.8.3
- @react-navigation/native 5.2.3
- @react-navigation/stack 5.2.18

#### References

- [Type checking with TypeScript](https://reactnavigation.org/docs/typescript/#type-checking-screens) - [React Navigation Documentation](https://reactnavigation.org/docs/getting-started)

---

React Navigation 의 [Stack Navigator](https://reactnavigation.org/docs/stack-navigator) 사용 시 Typescript 타입 지정에 관해 간략히 기록한다. 

#### createStackNavigator

`createStackNavigator` 메서드 사용 시 타입을 지정할 수 있다. 타입을 지정할 때는 구현하고자 하는 라우팅에 대해 [`Record`](https://www.typescriptlang.org/docs/handbook/utility-types.html#recordkt) 형식의 타입을 지정하면 된다.

```typescript
import { createStackNavigator } from '@react-navigation/stack';
export type RootStackParamList = {
  PictorialList: undefined // PictorialList 의 route.params 의 타입 지정. undefined 이면 params 를 사용하지 않겠다는 의미.
  PictorialDetail: {id: number | string} // PictorialDetail 의 route.params 의 타입 지정. params 로 id 값을 받겠다는 의미.
};
const Stack = createStackNavigator<RootStackParamList>();

// ...
```

#### 각 스크린

각 스크린으로 활용될 컴포넌트에서는 React Navigation 에게서 전달받은 `navigation`, `route` props 를 사용할 수 있다. 이들의 타입은 아래와 같이 지정할 수 있다. 위에서 작성해둔 `RootStackParamList`도 사용해야 한다.

```typescript
import { StackNavigationProp } from '@react-navigation/stack';
import { RouteProp } from '@react-navigation/native';
import RootStackParamList from '어딘가';

// ...

type PictorialDetailScreenProps = {
  navigation: StackNavigationProp<RootStackParamList, 'PictorialDetail'>
  route: RouteProp<RootStackParamList, 'PictorialDetail'>
}

const PictorialDetailScreen = ({
  route,
  navigation,
}: PictorialDetailScreenProps) => {

    ///...

}

export default PictorialDetailScreen;
```