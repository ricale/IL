# [Android] 리소스 없이 안드로이드 앱 아이콘 생성

#### References

- [Cool Text Generator](https://maketext.io/)
- [App Icon Generator](https://appicon.co/)

---

1. Cool Text Generator에서 문자열을 사용해 이미지를 만든다.
    - 폰트, 폰트의 그라데이션 색상, 배경 색상을 정할 수 있다.
    - PNG보다는 SVG를 추천한다.

2. 1에서 만든 이미지를 가지고 App Icon Generator 에서 앱 아이콘을 만든다.
    - 이미지를 하나 올리면 앱 아이콘을 해상도별로 만들어주는데, 1에서 PNG로 만들었을 경우 해상도가 낮아 이미지가 깨질 수 있다. 반면 SVG는 깨짐 없이 잘 생성된다.

3. 2의 결과물을 압축 파일로 다운받을 수 있다.
    - AppIcons.zip 파일이다. 압축을 풀면 AppIcons 폴더가 나온다.
    - AppIcons/playstore.png 파일은 구글 플레이 콘솔에서 앱을 등록할 때 사용한다.
    - AppIcons/android 디렉토리의 내용물은 안드로이드 프로젝트 폴더의 적절한 위치에 옮긴다.