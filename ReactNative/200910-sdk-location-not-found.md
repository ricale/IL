# [React Native][Android] SDK location not found.

#### Environment

- react-native 0.62

#### References

- [SDK location not found. Define location with sdk.dir in the local.properties file or with an ANDROID_HOME environment variable](https://stackoverflow.com/questions/27620262/sdk-location-not-found-define-location-with-sdk-dir-in-the-local-properties-fil) - Stack Overflow

---

아래와 같은 에러가 발생하며 빌드가 진행되지 않는다. (작업 컴퓨터를 변경하면서 생긴 에러)

> SDK location not found. Define location with an ANDROID_SDK_ROOT environment variable or by setting the sdk.dir path in your project's local properties file.

### 해결

`ROOT/android/local.properties` 파일을 만든다. 그리고 거기에 SDK 위치를 아래처럼 기록해주면 된다.

    sdk.dir = /Users/USERNAME/Library/Android/sdk

위 예시는 맥 기준 안드로이드 SDK의 기본 위치이므로 USERNAME만 적절히 변경해주면 된다. 만약 위와 다른 경로로 설치했는데 위치가 생각나지 않는다면, 안드로이드 스튜디오에서 확인할 수 있다. 환경설정의 [Appearance & Behavior] -> [System Settings] -> [Android SDK] 메뉴를 확인하자.
