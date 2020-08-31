# [React Native][Android] 한 프로젝트에서 여러 패키지 빌드

#### Environment

- react-native 0.62

#### References

- [빌드 변형 구성](https://developer.android.com/studio/build/build-variants) - Android Developers
- [Publishing to Google Play Store](https://reactnative.dev/docs/signed-apk-android) - React Native docs
- [React Native : Expiring Daemon because JVM heap space is exhausted?](https://stackoverflow.com/questions/59044161/react-native-expiring-daemon-because-jvm-heap-space-is-exhausted) - Stack Overflow
- [Gradle 4.0 Unable to find a matching configuration](https://stackoverflow.com/questions/44218614/gradle-4-0-unable-to-find-a-matching-configuration) - Stack Overflow
- 

---

하나의 프로젝트에서 두 개의 패키지를 얻어야 할 때가 있다. 예를 들면, 하나는 국내용(예, com.example.awesome)으로, 다른 하나는 해외용(예, com.example.awesome.global)으로 빌드를 나눠서 배포할 때다. 

서로 다른 패키지가 필요하다고 해서, 같은 내용의 프로젝트를 둘로 나눠서 관리하는 것은 좋은 방법이 아니다. 그것 보다는 빌드 시 옵션을 다르게 하는 방법으로 빌드 결과만 나누는 것이 좋다.

### `app/build.gradle`

안드로이드에서는 `app/build.gradle` 파일을 수정해서 쉽게 빌드를 나눌 수 있다. 아래는 `globaldebug`와 `globalrelease` 설정을 추가한 예시이다.

```gradle
    /// ...
    buildTypes {
        debug {
            // ...
        }
        release {
            // ...
        }
        globaldebug {
            initWith debug
            applicationIdSuffix ".global"
            matchingFallbacks = ['debug']
        }
        globalrelease {
            initWith release
            applicationIdSuffix ".global"
            matchingFallbacks = ['release']
        }
    }
    /// ...
```

- `applicationIdSuffix`: 어플리케이션 아이디(패키지 이름) 뒤에 추가로 붙을 문자열이다. 예를 들어 원래 패키지 이름이 `com.example.app` 이고 `applicationIdSuffix`가 `.global`이면 해당 환경의 패키지 이름은 `com.example.app.global`이 된다.
- `matchingFallbacks`: 앱내에서 사용되는 빌드 유형에 포함되지 않는, 새로운 빌드 유형을 위한 옵션이다. 새로운 빌드 유형 (위에서는 `globaldebug`, `globalrelease`)으로 빌드할 때, 빌드 유형 이름이 사용되는 코드에서는 각각의 빌드 유형 대신 `matchingFallbacks`에 기록된 빌드 유형 이름을 대체하여 사용한다.

### 빌드 명령어

`package.json` 에 빌드 명령어를 추가해서 좀 더 편하게 빌드할 수 있다.

```json
{
    // ...
    "scripts": {
        "android": "react-native run-android",
        "android-global": "react-native run-android --variant=globaldebug",
        "build-android": "cd android && ./gradlew assembleRelease",
        "build-android-global-test": "cd android && ./gradlew assembleGlobalrelease",
    },
    // ...
}
```