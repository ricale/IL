# [Android] Splash Screen

#### Environment

- Android Studio 3.6.2
- Android SDK (minVersion 21)

#### References

- [The (Complete) Android Splash Screen Guide](https://android.jlelse.eu/the-complete-android-splash-screen-guide-c7db82bce565) - Android Pub
- [How do I make a splash screen?](https://stackoverflow.com/questions/5486789/how-do-i-make-a-splash-screen) - Stack Overflow

---

Android 앱에 [스플래시 스크린](https://en.wikipedia.org/wiki/Splash_screen)을 구현하는 방법은 크게 두 가지가 있다.

1. 스플래시 스크린을 위한 theme 를 작성해 사용한 뒤, 로딩이 끝나면 앱 theme 로 바꿔치기 하는 것.
2. 스플래시 스크린을 위한 별도의 액티비티를 추가해 해당 액티비티를 먼저 띄운 뒤, 메인 액티비티로 이동하는 것.

theme 를 사용한 방법은
- 별도의 액티비티나 라우팅이 없기 때문에 코드가 깔끔하다.
- 앱 로딩이 끝나면 바로 화면을 전환해주기 때문에, 스플래시 스크린에 필요 이상 머무르지 않는다.

액티비티를 사용한 방법은
- 앱의 상태 (로그인 여부, 유저의 정보 및 상태) 에 따라 스플래시 스크린에서 알맞는 스크린으로 이동할 수 있다.
- 스플래시 스크린의 애니메이션 등으로 인해 (앱 로딩 시간 이상으로) 일정 시간 머무르게 하고 싶다면 타이머를 활용할 수 있다.

각각의 특징을 확인하고 맞는 방법을 사용하면 된다.