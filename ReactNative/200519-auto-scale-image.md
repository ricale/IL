# [React Native] 이미지 크기 지정

#### Environment

- React Native 0.62

#### References

- [Auto scale image height with React Native](https://stackoverflow.com/questions/42170127/auto-scale-image-height-with-react-native) - Stack Overflow
- [Image.getSize()](https://reactnative.dev/docs/image#getsize) - React Native Documentation

---

React Native 의 `Image` 컴포넌트는 `source` 속성으로 외부 URL을 넘겨줄 경우 이미지의 크기를 자동으로 계산하지 못한다 (로컬 파일 등 다른 경우에 대해서는 확인되지 않음). 따라서 `Image.getSize` 메서드를 통해 이미지의 크기를 가져와야 한다.

```javascript
const ImageWithFullWidth = ({imgUrl}) => {
    // ...
    const [size, setSize] = useState({width: 0, height: 0});
    const screenWidth = Dimensions.get('screen').width;
    Image.getSize(
        imgUrl,
        (width, height) => { // success callback
            setSize({width, height});
        },
        (error) => {} // failure callback
    )

    // ...

    return (
        <Image
            source={{uri: imgUrl}}
            style={{
                width: screenWidth,
                height: screenWidth * size.width / size.height
            }}
            />
    )
}
```
