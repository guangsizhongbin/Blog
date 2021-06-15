---
title: "15_date"
date: 2021-04-15T21:58:11+08:00
lastmod: 2021-04-15
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### What's the different between `Date` class and `LocalDate` class?

`Date` class:

which represents a point in time

`LocalDate` class:

which expresses days in the familiar calendar notation

```java
public class InputTest {
    public static void main(String[] args) {
        System.out.println(LocalDate.now().plusDays(1));
        System.out.println(LocalDate.of(1999, 12, 31));

        System.out.println(new Date().toString());
    }
}
```

![20210507221636](https://img.fengqigang.cn//img/20210507221636.png)

### 如何实现 **Data** 的匹配模式?

**SimpleDateFormat** is a concrete class for formatting and parsing dates in a locale-sensitive manner. It allows for formatting (date -> text), parsing (text -> date), and normalization.

**parse**

Parse a date/time string according to the given parse position

```java
public class Demo {
    public static void main(String[] args) throws IOException, ParseException {
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy/MM/dd HH:mm:ss");

        //1. 格式化
        Date d = new Date(3742762088000L);
        String timeStr = sdf.format(d);
        System.out.println(timeStr);

        //2.解析
        String time = "2077/07/07 07:07:07";
        Date parse = sdf.parse(time);
        System.out.println(parse.getTime());

    }
}
```

![20210415210434](https://img.fengqigang.cn//img/20210415210434.png)

### 如何计算现在到1970年多少年了? 并返回当时的时间?

**public void setTime(long date)**

Set an existing Date object using the given milliseconds time value.

```java
public class Demo {
    public static void main(String[] args) {
        Date d = new Date();
        long time = d.getTime();
        System.out.println(time / (1000L * 3600 * 24 * 365));

        d.setTime(0);
        System.out.println(d);
    }
}
```

![20210415215456](https://img.fengqigang.cn//img/20210415215456.png)

