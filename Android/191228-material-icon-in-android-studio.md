# Android 프로젝트에 Material 디자인 아이콘 추가

#### Environment

- Android Studio 3.5.3
- Android SDK (minVersion 21)

####References

- [Import material design icons into an android project](https://stackoverflow.com/questions/28684759/import-material-design-icons-into-an-android-project) - Stack Overflow
- [Why is my FloatingActionButton icon black?](https://stackoverflow.com/questions/53458821/why-is-my-floatingactionbutton-icon-black/53668350) - Stack Overflow

---

### 1. 프로젝트에 아이콘 추가

Android Studio를 사용해서 Android를 개발할 때, Material 디자인의 아이콘을 사용할 수 있다. 하지만 기본적으로 프로젝트에 추가되어있지 않기 때문에, 추가하는 과정을 거쳐야 한다. Vector Asset Studio를 사용하면 되는데, 이 글의 답변에 잘 요약되어 있기 때문에 해당 부분을 인용한다.

> 아래 과정을 따라서 Vector Asset Studio를 켜세요
>
> - Android Studio에서, 프로젝트를 여세요.
> - Project 윈도우에서, Android view를 선택하세요.
> - res 폴더를 우클릭한 뒤, New > Vector Asset을 선택하세요.
>
> Vector Asset Studio를 켜면, 프로젝트에 Material 아이콘을 추가할 수 있어요.
>
> - "Material Icon"을 선택하세요 (Clip Art 항목의 아이콘 이미지를 클릭하시면 됩니다)
> - 아이콘을 선택하세요.

### 2. 아이콘의 색상 지정

아이콘을 추가할 때 색상도 정할 수 있는데, 특정 상황에서는 아이콘의 색상이 무시될 때가 있다. 대표적인 예가 `FloatingActionButton` 에 `src` 속성으로 아이콘을 지정했을 때이다. 아이콘 색상이 (테마에 따라 다를 수 있지만) 검은색으로 나오게 되는데, 그럴 때는 `android:tint`(혹은 `app:tint`) 속성을 통해 색상을 별도로 지정해주면 된다.