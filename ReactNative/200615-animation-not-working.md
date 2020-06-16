# [React Native] Transform with key of "translateY" must be a number: {"translateY":0}

#### Environment

- React Native 0.62

#### References

- [Animated not working with translate: Transform with key of "translateY" must be a number: {"translateY":0}](https://github.com/facebook/react-native/issues/11503)

---

```jsx
<View
    style={{
        transform: [
            {translateX: scrollInfo.scrollPosXAnim}
        ]
    }}
    // ...
    />
```

위처럼 View 에 애니메이션 속성 지정시 아래와 같은 에러가 발생한다.

> Transform with key of "translateY" must be a number: {"translateY":0}

에러가 나는 이유는 `View` 컴포넌트가 애니메이션을 지원하지 않기 때문이다. `Animated.View`를 사용하자.

```jsx
<Animated.View
    style={{
        transform: [
            {translateX: scrollInfo.scrollPosXAnim}
        ]
    }}
    // ...
    />
```
