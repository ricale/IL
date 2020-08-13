# [React Native] iOS 빌드 에러 (We ran "xcodebuild" command but it exited with error code 65)

#### Environment

- react-native 0.62

#### References

- [Xcode 10 Error: Multiple commands produce][https://stackoverflow.com/questions/50718018/xcode-10-error-multiple-commands-produce]

---

iOS 빌드 (`yarn react-native run-ios`) 가 갑자기 아래와 같은 에러를 내며 진행되지 않았다.

> Failed to build iOS project. We ran "xcodebuild" command but it exited with error code 65. To debug build logs further, consider building your app with Xcode.app, by opening leeheeExpressReactNative.xcworkspace

해당 메시지로 구글에서 검색을 해보면 [이 Stack Overflow 의 글](https://stackoverflow.com/questions/55235825/error-failed-to-build-ios-project-we-ran-xcodebuild-command-but-it-exited-wit)과 [react-native 레파지토리의 이슈](https://github.com/facebook/react-native/issues/25240) 등이 상단에 나오는데, 두 글을 포함한 대부분의 글이 대체로 아래의 두 가지의 방법을 제시한다.

- 빌드 캐시 (PROJECT_ROOT/ios/build) 를 삭제한 뒤 다시 빌드.
- Xcode 의 Workspace Settings 에서 빌드 시스템을 Legacy Build System 으로 변경.

하지만 두 방법으로 해결되지 않았다.

Xcode 로 빌드를 해도 에러가 나는 것은 같았다. 하지만 에러 메시지가 달랐다.

> Multiple commands produce '/Users/me/Library/Developer/Xcode/DerivedData/myReactNativeProject-gtmgyeksivfuokbcecnvxgepzwaa/Build/Products/Debug-iphoneos/myReactNativeApp.app/GoogleService-Info.plist':
> 1) Target 'myReactNativeProject' (project 'myReactNativeProject') has copy command from '/Users/me/Downloads/GoogleService-Info.plist' to '/Users/me/Library/Developer/Xcode/DerivedData/myReactNativeProject-gtmgyeksivfuokbcecnvxgepzwaa/Build/Products/Debug-iphoneos/myReactNativeApp.app/GoogleService-Info.plist'
> 2) Target 'myReactNativeProject' (project 'myReactNativeProject') has copy command from '/Users/me/workspace/leehee/myReactNativeProject/ios/GoogleService-Info.plist' to '/Users/me/Library/Developer/Xcode/DerivedData/myReactNativeProject-gtmgyeksivfuokbcecnvxgepzwaa/Build/Products/Debug-iphoneos/myReactNativeApp.app/GoogleService-Info.plist'

firebase 를 적용하기 위해 GoogleService-Info.plist 파일을 추가할 때 문제가 생긴 모양이었다.

[이 글](https://stackoverflow.com/questions/50718018/xcode-10-error-multiple-commands-produce)을 보니 `Build phases` > `Copy Bundle Resources` 에서 plist 파일을 삭제하라고 나온다. 

그렇게 하니 해결되었다.

덧붙여 위에서 제시되었던, "빌드 시스템을 Legacy Build System 으로 변경"하는 방법은, 문제를 해결하는 것이 아닌 회피하는 방안이니 (에러 메시지가 일시적으로 안나게만 하는 방법이니) 권장되지 않는다고 한다.
