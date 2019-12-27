# DatePickerDialog 색상 변경

#### References

- [How to change DatePicker dialog color for Android 5.0](https://stackoverflow.com/questions/28738089/how-to-change-datepicker-dialog-color-for-android-5-0) - Stack Overflow

---

본래는 Dialog에 DatePicker를 올려서 사용했었으나, DatePickerDialog만으로도 원하는 기능을 구현하기에는 충분하고, DatePicker의 색상 변경은 원하는 적절한 방법을 찾지 못했기 때문에 DatePickerDialog로 변경했다.

DatePickerDialog는 styles.xml에 속성을 추가함으로써 쉽게 색상을 변경할 수 있다.

```xml
<style name="AppTheme" parent="Theme.MaterialComponents.DayNight">
  <!-- ... -->
  <item name="android:datePickerDialogTheme">@style/MyDatePickerDialogTheme</item>
  <!-- ... -->
</style>

<style name="MyDatePickerDialogTheme" parent="android:Theme.Material.Dialog">
    <item name="android:colorAccent">#FFF</item>
    <item name="android:buttonBarNegativeButtonStyle">@style/NegativeButtonStyle</item>
    <item name="android:buttonBarPositiveButtonStyle">@style/PositiveButtonStyle</item>
</style>

<style name="NegativeButtonStyle" parent="Widget.MaterialComponents.Button.TextButton.Dialog">
</style>
<style name="PositiveButtonStyle" parent="Widget.MaterialComponents.Button.TextButton.Dialog">
</style>
```

위 문서의 세 속성 말고도 아래와 같은 속성들이 있다.

```
dayOfWeekBackground
dayOfWeekTextAppearance
headerMonthTextAppearance
headerDayOfMonthTextAppearance
headerYearTextAppearance
headerSelectedTextColor
yearListItemTextAppearance
yearListSelectorColor
calendarTextColor
calendarSelectedTextColor
```

