# [Android] swipe 액션 탐지

#### Environment

- Android Studio 3.5.3
- Android SDK (minVersion 21)

#### References

- [How to detect the swipe left or Right in Android?](https://stackoverflow.com/questions/6645537/how-to-detect-the-swipe-left-or-right-in-android) - Stack Overflow

---

출처의 코드는 좌우 스와이프 탐지 코드이고, 아래 코드는 위아래 스와이프 감지 코드이다.

```kotlin
class SomeActivity : AppCompatActivity() {
    companion object {
        // ...
        const val MIN_DISTANCE_SWIPE = 100
        // ...
    }
    // ...

    private var touchDownY = 0.0f
    private var touchUpY = 0.0f

    //...

    override fun onTouchEvent(event: MotionEvent?): Boolean {
        when(event?.action) {
            MotionEvent.ACTION_DOWN -> {
                touchDownY = event.y
            }
            MotionEvent.ACTION_UP -> {
                touchUpY = event.y
                if(MIN_DISTANCE_SWIPE < touchDownY - touchUpY) {
                    doSomething()
                }
            }
        }
        return super.onTouchEvent(event)
    }

    // ...
}
```
