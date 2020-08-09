# [React Native] React Navigation 타입 지정

#### Environment

- react-native 0.62
- react-native-webview 10.2.3

#### References

- [Source.headers is not supported when using POST](https://stackoverflow.com/questions/52590425/source-headers-is-not-supported-when-using-post)

---

react-native-webview 의 `source.method` 로 POST를 지정하면, `source.headers` 를 지정할 수 없게 된다. (iOS는 된다. 안드로이드만 안 된다.)

헤더를 넣어주기 위해서는 `fetch` 메서드를 활용하면 된다. 해당 메서드로 요청을 날린뒤, 돌아온 응답 HTML 을 웹뷰에 고스란히 넣어주자.

```tsx
const SomeComp = ({bodyObj}) => {
    const body = useMemo(() =>
        Object.keys(bodyObj).map(key =>
            `${key}=${bodyObj[key]}`
        ).join('&')
    , [bodyObj]);

    const [html, setHtml] = useState('');
    useEffect(() => {
        if(body) {
            fetch(SOME_URI, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/x-www-form-urlencoded',
                },
                body,
            }).then(res =>
                res.text()
            ).then(text =>
                setHtml(text)
            );
        }
    }, [body]);

    if(!html) {
        return null;
    }

    return (
        <WebView
            source={{
                html,
                baseUrl: SOME_URI,
            }}
            // ...
            />
    )
}
```