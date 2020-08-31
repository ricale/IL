# [TypeScript] generic 타입의 컴포넌트에 styled-components 적용 시 타입 에러

#### Environment

- typescript 3.8.3
- styled-components 5.1.0

#### References

- [\[TypeScript\] styled wrapper doesn't preserve generic props](https://github.com/styled-components/styled-components/issues/1803)

---

(__아래 해결책은 예시로 든 `FlatList` 뿐만 아니라, generic 타입을 사용하는 모든 컴포넌트에 적용될 수 있다.__)

styled-components 로 `FlatList`를 만들 경우, 사용 시 타입 에러가 발생한다.

```tsx
const StyledFlatList = styled(FlatList)`
  padding-left: 10px;
  padding-right: 10px;
`;

// ....

<StyledFlatList
    data={data}
    // renderItem 의 item 의 타입은
    // data 어트리뷰트와 관계 없이 무조건 unknown 이다.
    renderItem={({item /* unknown */, index}) =>
        <Item
            item={item}
            onPress={onPressItem}
            />
    }
    // renderItem 과 마찬가지다.
    // keyExtractor 의 item 의 타입은
    // data 어트리뷰트와 관계 없이 무조건 unknown 이다.
    keyExtractor={(item /* unknown */, index) => `${item?.id}`}
    />
```

typescript 의 문제인 건지 styled-components 의 문제인 건지 정확히는 알 수 없다.

여하튼 이 문제는 styled-components 사용 시 타입 지정을 좀 더 세밀하게 함으로써 해결할 수 있다.

```tsx
const List = styled(FlatList)`
  padding-left: ${p => p.theme.dimens.margin}px;
  padding-right: ${p => p.theme.dimens.margin}px;
` as React.ComponentType as new <T>() => FlatList<T>;
```

코드가 깔끔하지 않아 썩 마음에 드는 해결책은 아니지만, 일단 typescript 에러를 없앤 것으로 만족하기로 한다.
