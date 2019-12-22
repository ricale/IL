# 두 개의 LocalDate 객체 간의 차이(일) 구하기

#### References

- [java 8 – how to calculate difference between two dates or java.time.LocalDate instances](https://www.javabrahman.com/java-8/java-8-how-to-calculate-difference-between-two-java-time-localdate-instances/) - javabrahman.com

---

Java의 `java.time.LocalDate` 클래스는 날짜를 표현하는 클래스이다. 서로 다른 두 `LocalDate` 객체의 차이를 구하는 방법이 많이 있는데 그 중 하나가 `java.time.Period` 클래스를 사용하는 것이다.

```java
LocalDate dateA = LocalDate.of(2015, 1, 12);
LocalDate dateB = LocalDate.of(2016, 3, 22);
 
Period intervalPeriod = Period.between(dateA, dateB);
System.out.println(period);             // P1Y1M19D                                                                                                               
System.out.println(period.getDays());   // 19
System.out.println(period.getMonths()); // 1
System.out.println(period.getYears());  // 1
```

하지만 이 클래스는 몇 년 몇월 며칠이 차이 나는 지를 보여주지, 총 며칠이 차이인지를 알려주지는 않는다.

총 며칠 차이인지 알고 싶을 때는 `java.time.temporal.ChronoUnit.DAYS` 를 사용하면 된다.

```java
LocalDate dateA = LocalDate.of(2018, 11, 3);
LocalDate dateB = LocalDate.of(2019, 12, 22);
Long days = ChronoUnit.DAYS.between(dateA, dateB);
System.out.println(days); // 414
```

