# [React Native] 안드로이드 빌드 에러 (... due to missing strip tool for ...)

#### Environment

- react-native 0.62

#### References

- [init new project and react-native run-android can't work in RN 0.62.0 & 0.62.1][answer]

---

아래와 같은 정체불명의 에러들이 뜨면서, 안드로이드 빌드가 진행되지 않을 때가 있다.

> '/프로젝트경로/android/app/build/intermediates/merged_native_libs/release/out/lib/armeabi-v7a/퍄일명' due to missing strip tool for ABI 'ARMEABI_V7A'. Packaging it as is.
> '/프로젝트경로/android/app/build/intermediates/merged_native_libs/release/out/lib/armeabi-v7a/퍄일명' due to missing strip tool for ABI 'ARMEABI_V7A'. Packaging it as is.
> '/프로젝트경로/android/app/build/intermediates/merged_native_libs/release/out/lib/armeabi-v7a/퍄일명' due to missing strip tool for ABI 'ARMEABI_V7A'. Packaging it as is.
> .... 반복

위 메시지에서 armeabi-v7a 부분과 ARMEABI_V7A 부분을 X86, ARM64_V8A 등으로 바뀐 메시지들도 주르륵 같이 뜬다.

처음에는 gradle 을 업그레이드 하면 되는 것인 줄 알고 업그레이드했고 실제로 해결되기도 했었는데, 결과적으로 임시방편이었다.

[이 답변][answer]을 보면 Gradle 데몬이 중복적으로 실행되고 있어 생기는 문제라고 한다. 해당 데몬을 찾아서 프로세스를 죽이고 빌드하니 이제 정상적으로 진행된다.

```bash
$ cd android && ./gradlew  --status # gradle daemon 목록이 보임
$ kill 5823 # 해당 데몬의 PID(여기서는 5823)를 이용해 프로세스를 죽임
```

[answer]: https://github.com/facebook/react-native/issues/28541