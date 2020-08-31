# [React] Warning: This synthetic event is reused for performance reasons

#### Environment

- react 16.13.1

#### References

- [React SyntheticEvent reuse](https://medium.com/trabe/react-syntheticevent-reuse-889cd52981b6#:~:text=%E2%80%9CWarning%3A%20This%20synthetic%20event%20is,we%20cannot%20access%20its%20properties.)

---

```tsx
const SomeComponent = () => {
    const [info, onChangeInfo] = useState({name: '', age: 0});
    const onChangeName = useCallback((event) => {

    })
    return (
        <div>
            <input
                value={name}
                onChange={event => {
                    onChangeInfo(info => ({
                        ...info,
                        name: e.target.value,
                    }))
                }}
                />
        </div>
    );
}
```

위처럼 코드를 짜면 아래와 같은 경고와 함께 코드가 정상적으로 동작하지 않는다.

> Warning: This synthetic event is reused for performance reasons

이유는 React 의 _`SyntheticEvent`_ 객체에 비동기 메서드로 접근하려 했기 때문이다. 이벤트 객체 재사용을 이유로, 이벤트 콜백이 종료되는 시점에서 기존의 이벤트 객체는 더이상 유효하지 않게 된다. 정확한 이유는 알 수 없으나, 최적화와 관련된 이슈라고 생각된다.

가장 간단한 해결 방법은, 사용하고자 하는 값을 별도의 변수에 넣어서 클로저에서 접근 가능하게 하는 것이다.

```tsx
const SomeComponent = () => {
    const [info, onChangeInfo] = useState({name: '', age: 0});
    const onChangeName = useCallback((event) => {

    })
    return (
        <div>
            <input
                value={name}
                onChange={event => {
                    const {value} = event.target; // <-
                    onChangeInfo(info => ({
                        ...info,
                        name: value,
                    }))
                }}
                />
        </div>
    );
}
```

[`event.persist()` 메서드를 사용하는 방법](https://reactjs.org/docs/events.html#event-pooling)도 있다. 해당 내용은 문서를 참고하시라.
