# SharedPreferences.Editor 의 apply와 commit의 차이

#### Environment

- Android Studio 3.5.3
- Android SDK (minVersion 21)

#### References

- [What's the difference between commit() and apply() in Shared Preference](https://stackoverflow.com/questions/5960678/whats-the-difference-between-commit-and-apply-in-shared-preference) - Stack Overflow
- [SharedPreferences.Editor](https://developer.android.com/reference/android/content/SharedPreferences.Editor.html#apply()) - Android Developers

---

간단히 요약하면 아래와 같다.

- apply`: 결과값을 반환하지 않고 비동기적으로 처리
- `commit`: 결과값(true or false)을 반환하는 동기적 처리

아래는 [apply 메서드의 공식 문서](https://developer.android.com/reference/android/content/SharedPreferences.Editor.html#apply())에서 발췌한 내용이다.

> Unlike `commit()`, which writes its preferences out to persistent storage synchronously, `apply()` commits its changes to the in-memory `SharedPreferences` immediately but starts an asynchronous commit to disk and you won't be notified of any failures. If another editor on this `SharedPreferences` does a regular `commit()` while a `apply()` is still outstanding, the `commit()` will block until all async commits are completed as well as the commit itself.

공식 문서에 따르면 `apply`는 인메모리에 동기적으로 저장한 뒤 디스크에 비동기적으로 저장한다고 한다. 설령 다른 SharedPreferences.Editor에 의한 `apply` 혹은 `commit` 이 와도, 해당 데이터에 관한 적절한 블록이 적용되기 때문에 데이터에는 문제가 없다고 한다.

따라서 기왕이면 `commit`보다는 (조금 더 빠른) `apply`를 쓰자. (commit을 쓰면 Android Studio에서 lint 경고를 보여준다.)