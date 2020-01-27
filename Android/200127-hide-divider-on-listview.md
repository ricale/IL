# [Android] ListView에서 divider 제거

#### References

- [How do I remove lines between ListViews on Android?](https://stackoverflow.com/questions/1914477/how-do-i-remove-lines-between-listviews-on-android) - Stack Overflow

---

클래스 상에서

```java
getListView().setDivider(null);
getListView().setDividerHeight(0);
```

XML 상에서

```xml
<ListView
    ...
    android:divider="@null"
    android:dividerHeight="0dp"
    ...
    />
```
