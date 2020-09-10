# [React Native][iOS] .xcconfig unable to open file

#### Environment

- react-native 0.62

#### References

- [Xcode, Pods ProjectName.debug.xcconfig unable to open file. Wrong directory][answer] - 사이트

---

아래와 같은 에러가 발생하며 빌드가 진행되지 않는다. (작업 컴퓨터를 변경하면서 생긴 에러)

> projectName/Pods/Pods...ProjectName.debug.xcconfig unable to open file

(에러 메시지는 [위 출처][answer]의 글에서 가져왔다. 내가 직접 확인한 에러는 따로 기록해두지 않아서 확인할 수 없다.)

### 해결

1\. 아래 명령어를 실행한다.

```bash
pod deintegrate
```

2\. `ios/PROJECT_NAME.xcodeproj/project.pbxproj` 파일에서 `path = Pods` 부분을 찾아서 `name = Pods` 로 변경해준다.

3\. 아래 명령어를 실행한다.

```bash
pod install
```


[answer]: https://stackoverflow.com/questions/55558984/xcode-pods-projectname-debug-xcconfig-unable-to-open-file-wrong-directory