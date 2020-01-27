# [Android] transition 애니메이션 적용

#### Environment

- Android Studio 3.5.3
- Android SDK (minVersion 21)

#### References

- [속성 애니메이션 개요](https://developer.android.com/guide/topics/graphics/prop-animation) - Android Developers
- [Basics of Easing Animations in android](http://shrikanth.in/android/2015/11/12/easing-animations-android.html) - shrikanth.in
- [Android easing functions](https://gist.github.com/jacksonej/e635fc497b7627689050) - GitHub gist

---

출처의 코드들을 참고해 작성함

`SomeActivity.kt`

```kotlin
// ...
import android.animation.AnimatorSet
// ...

class SomeActivity : AppCompatActivity() {
    companion object {
        // ...
        const val SWIPE_ANIM_DURATION = 500L
        private const val SWIPE_ANIM_TOP_RATE = 0.0f
        private const val SWIPE_ANIM_BOTTOM_RATE = 1.0f
        // ...
    }

    // ...

    private lateinit var guideline: Guideline
    private lateinit var startAnimatorSet: AnimatorSet
    private lateinit var endAnimatorSet: AnimatorSet

    // ...

    private fun showWidget() {
        startAnimatorSet.start()
    }

    private fun hideWidget() {
        endAnimatorSet.start()
    }

    private fun setAnimation() {
        startAnimatorSet = AnimatorFactory.create(
            SWIPE_ANIM_BOTTOM_RATE,
            SWIPE_ANIM_TOP_RATE,
            SWIPE_ANIM_DURATION
        ) {
            guideline.setGuidelinePercent(it.animatedValue as Float)
        }

        endAnimatorSet = AnimatorFactory.create(
            SWIPE_ANIM_TOP_RATE,
            SWIPE_ANIM_BOTTOM_RATE,
            SWIPE_ANIM_DURATION
        ) {
            guideline.setGuidelinePercent(it.animatedValue as Float)
        }
    }

    // ...
}
```

`AnimatorFactory.kt`

```kotlin
import android.animation.AnimatorSet
import android.animation.ValueAnimator

// TODO: make more generic if needed
object AnimatorFactory {
    fun create(
        startValue: Float,
        endValue: Float,
        duration: Long,
        listener: (ValueAnimator) -> Unit
    ): AnimatorSet {
        val animatorSet = AnimatorSet()
        val valueAnimator = ValueAnimator.ofFloat(startValue, endValue)
        valueAnimator.setEvaluator(EasingEvaluator(duration.toFloat()))
        valueAnimator.addUpdateListener(listener)
        animatorSet.playTogether(valueAnimator)
        animatorSet.duration = duration

        return animatorSet
    }
}
```

`EasingEvaluator.kt`

```kotlin
import android.animation.TypeEvaluator

class EasingEvaluator(val duration: Float): TypeEvaluator<Number> {

    override fun evaluate(fraction: Float, startValue: Number, endValue: Number): Float {
        return calculate(
            duration * fraction,
            startValue.toFloat(),
            endValue.toFloat() - startValue.toFloat(),
            duration
        )
    }

    private fun calculate(tOrig: Float, b: Float, c: Float, d: Float): Float{
        val t = tOrig / d
        return c * t * t + b;
    }
}
```
