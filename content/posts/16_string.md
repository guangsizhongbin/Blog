---
title: "16_string"
date: 2021-04-16T21:49:13+08:00
lastmod: 2021-04-16
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### How to convert a String to an integer?

Integer.paraseInt(s);

```java
public class StringToInt {
    public static void main(String[] args) {
        String num = "1234";
        int x = Integer.parseInt(num);
        System.out.println(x);
    }
}
```

![20210511222008](https://img.fengqigang.cn//img/20210511222008.png)

### What boxing and unboxing is courtesy of ?

Boxing and unboxing is a courtesy of the complier, not the virtual machine

**source file**

```java
public class TestBoxing {
    public static void main(String[] args) {
        Integer n = 1;
        Float x = 2.0f;
        System.out.println(true ? n : x);
    }
}
```

**after complie**

```java
public class TestBoxing {
    public TestBoxing() {
    }

    public static void main(String[] args) {
        Integer n = 1;
        Float x = 2.0F;
        System.out.println((float)n);
    }
}
```

### 在进行深拷贝时，如何实现一个空接口？

**Cloneable** 并不是自己实现的

![](https://img.fengqigang.cn//img/20210413154201.png)

### ![](https://img.fengqigang.cn//img/20210413154436.png) 如何将byte数组转成 String, 并输出它

![](https://img.fengqigang.cn//img/20210413154534.png)

### 在 **JDK** 源码当中， 涉及区间的方法，一般都是怎么规定区间的?

左闭右开

这种做法是为了适配数组从0开始的下标

### ![20210413195347](https://img.fengqigang.cn//img/20210413195347.png)会输出什么?

会直接输出整个 **String**

![20210413195413](https://img.fengqigang.cn//img/20210413195413.png)

### **String** 对象中的不可变性，**JVM** 内存图是什么样的?

![20210413195747](https://img.fengqigang.cn//img/20210413195747.png)

### **静态常量池** 是干什么的?

在用字面值常量给 **String** 对象赋值时，在编译时期就加入了 **常量池**

当常量池中已存在某位字符串对象时，当需要使用时，就不需要在堆上重新创建对象了，而是直接去指向这个常量池中的字符串对象

### ![20210413200235](https://img.fengqigang.cn//img/20210413200235.png) 它们的值是什么?

![20210413200317](https://img.fengqigang.cn//img/20210413200317.png)

s.equals(s2) 是根据值来判断的

### ![20210413200627](https://img.fengqigang.cn//img/20210413200627.png) 它们会输出什么?

s3 == (s1 + s2) 肯定不能编译确定取值，必须运行期确定，那么它的对象就一定不在常量池，而在堆上

### 判断一个字符串是否为空可以采取什么样的方法?

**equals**

```java
public class supertest {
    public static void main(String[] args) {
        String s = "abc";
        System.out.println("".equals(s));
    }
}
```

![20210413201101](https://img.fengqigang.cn//img/20210413201101.png)

如果s是**null**, 会导致报错

### ![20210413201156](https://img.fengqigang.cn//img/20210413201156.png) 如何比较这两个字符串，并忽略大小写?

**a.equalsIgnoreCase(b)**

```java
public class supertest {
    public static void main(String[] args) {
        String s = "abc";
        String s1 = "ABC";
        System.out.println(s.equalsIgnoreCase(s1));
    }
}
```

![20210413201337](https://img.fengqigang.cn//img/20210413201337.png)

### ![20210413201420](https://img.fengqigang.cn//img/20210413201420.png) 如何判断这个字符串否包含a?

```java
public class supertest {
    public static void main(String[] args) {
        String s = "abc";
        System.out.println(s.contains("a"));
    }
}
```

![20210413201507](https://img.fengqigang.cn//img/20210413201507.png)

### ![20210413201524](https://img.fengqigang.cn//img/20210413201524.png) 如何判断其是否以a开头?

**a.startsWith("a")**

```java
public class supertest {
    public static void main(String[] args) {
        String s = "abc";
        System.out.println(s.startsWith("a"));
    }
}
```

![20210413201629](https://img.fengqigang.cn//img/20210413201629.png)

### ![20210413201524](https://img.fengqigang.cn//img/20210413201524.png) 如何判断其是否以c结尾?

**a.endsWith("c")**

```java
public class supertest {
    public static void main(String[] args) {
        String s = "abc";
        System.out.println(s.endsWith("c"));
    }
}
```

![20210413201816](https://img.fengqigang.cn//img/20210413201816.png)

### ![20210413202041](https://img.fengqigang.cn//img/20210413202041.png) 如何输出其子字符串 **world** ?

```java
public class supertest {
    public static void main(String[] args) {
        String s = "hello world";
        System.out.println(s.substring(6, s.length()));
    }
}
```

![20210413202308](https://img.fengqigang.cn//img/20210413202308.png)

### ![20210413202848](https://img.fengqigang.cn//img/20210413202848.png) 其会输出什么?

它会输出一个 **Arrays**, 里面的元素是 abc, 对应的编码值

![20210413202935](https://img.fengqigang.cn//img/20210413202935.png)

### ![20210413203145](https://img.fengqigang.cn//img/20210413203145.png) 其会输出什么?

它会输出一个 **Arrays**, 里面的元素是 a, b, c

![20210413203259](https://img.fengqigang.cn//img/20210413203259.png)

### ![20210413203402](https://img.fengqigang.cn//img/20210413203402.png) 其会输出什么?

它会输出一个 **字符串**

![20210413203434](https://img.fengqigang.cn//img/20210413203434.png)

### ![20210413204054](https://img.fengqigang.cn//img/20210413204054.png) 其会输出什么?

**toLowerCase()**, **toUpperCase()**

![20210413204130](https://img.fengqigang.cn//img/20210413204130.png)

### ![20210413204515](https://img.fengqigang.cn//img/20210413204515.png) 如何将字符串s3全部以字符形式加入c2?

**getChars(int srcBegin, int srcEnd, char\[\] dst, int dstBegin)**

```java
public class supertest {
    public static void main(String[] args) {
        char[] c2 = new char[20];
        System.out.println(Arrays.toString(c2));
        String s3 = "我真是一个小天才儿童手表!";
        s3.getChars(0, s3.length(), c2, 0);
        System.out.println(Arrays.toString(c2));
    }
}
```

![20210413204648](https://img.fengqigang.cn//img/20210413204648.png)

### ![20210413204733](https://img.fengqigang.cn//img/20210413204733.png) 如何将 **hellq** 中的 **q** 转换成 **o**

**String replace(char old, char new)**

![20210413204949](https://img.fengqigang.cn//img/20210413204949.png)

![20210413204957](https://img.fengqigang.cn//img/20210413204957.png)

### ![20210413205035](https://img.fengqigang.cn//img/20210413205035.png) 如何删除字符串左右的空格?

**a.trim()**

```java
public class supertest {
    public static void main(String[] args) {
        String a = "    hello    ";
        String a1 = a.trim();
        System.out.println(a1);
    }
}
```

![20210413205138](https://img.fengqigang.cn//img/20210413205138.png)

### **Comparable** 接口是干什么的?

**String** 类是一个实现了 **Comparable** 接口的类

所有实现 **Comparable** 接口的类， 都可以通过 **Arrays.sort(数组)** 或者 **Collections**, **sort** 集合进行排序

这种排序称之为 **自然排序**

**compareTo** 方法被称为它的 **自然比较方法**

### 如何实现按照年龄大小进行排序?

```java
public class supertest {
    public static void main(String[] args) {
        Student[] studs = new Student[3];
        Student s1 = new Student(11, 2, "123");
        Student s2 = new Student(132, 7, "1223");
        Student s3 = new Student(21, 1, "12333");
        Student s4 = new Student(51, 4, "1231231");
        Student s5 = new Student(61, 2, "125343");
        Student[] stud = {s1, s2, s3, s4, s5};
        System.out.println(Arrays.toString(stud));
        Arrays.sort(stud);
        System.out.println(Arrays.toString(stud));
    }
}


class Student implements Comparable {
    int age;
    int id;
    String name;

    public Student() {
    }

    public Student(int age, int id, String name) {
        this.age = age;
        this.id = id;
        this.name = name;
    }
}
```

![20210413210740](https://img.fengqigang.cn//img/20210413210740.png)

从小到大， 左减去右

```java
public class supertest {
    public static void main(String[] args) {
        Student[] studs = new Student[3];
        Student s1 = new Student(11, 2, "123");
        Student s2 = new Student(132, 7, "1223");
        Student s3 = new Student(21, 1, "12333");
        Student s4 = new Student(51, 4, "1231231");
        Student s5 = new Student(61, 2, "125343");
        Student[] stud = {s1, s2, s3, s4, s5};
        System.out.println(Arrays.toString(stud));
        Arrays.sort(stud);
        System.out.println(Arrays.toString(stud));
    }
}


class Student implements Comparable {
    int age;
    int id;
    String name;

    public Student() {
    }

    public Student(int age, int id, String name) {
        this.age = age;
        this.id = id;
        this.name = name;
    }

    @Override
    public int compareTo(Object o) {
        Student targetStu = (Student) o;
        return this.age - targetStu.age;
    }

    @Override
    public String toString() {
        return "age=" + age;
    }
}
```

![20210413210818](https://img.fengqigang.cn//img/20210413210818.png)

### 除了 **compareTo** 方法，类中还有 **equals** 方法判断两个对象是否相等, 建议这两个方法同 **true** 同 **false** , 应该如何做到?

![20210413211037](https://img.fengqigang.cn//img/20210413211037.png)

只需要做到 **age** 相等即可

必须保证 **equals()** 方法重写和 **compareTo()** 方法重写保持一致的方式

### 常用的自然排序的方法是什么?

**Comparable** 接口实现自然排序麻烦且不方便

使用带 **Comparator** 比较器的 **sort** 方法， ( **Arrays** 和 **Collections**) 中都有该方法

### 在 **Comparator** 接口中有两个抽象方法 **compare** 和 **equals**, 为什么它还是抽象方法?

接口的实现类一定还继承了 **Object**

所以抽象方法 **equals** 不需要实现， 它只需要实现一个抽象方法 **compare** , 它仍然是功能接口

### 在 **Comparator** 接口中有两个抽象方法 **compare** 和 **equals**, 为什么还要多写一个 **equals**?

这里把 **equals** 方法作为一个抽象方法是提示你重写它，如果不重写可能会有些矛盾

### 自然排序在开发中有什么作用?

1.  用 SQL 操作数据库， 然后进行排序 (SQL排序) , 这种做法是常用的，但SQL有时候会有效率问题
    
2.  一旦 SQL 的排序出现了效率问题，而一时没有太好的办法解决
    

可以先把数据读到集合当中，然后对集合进行自然排序，然后把数据返还给前端，所以自然排序有时候可以用来解决 **SQL** 排序的效率问题

### What's the difference between `code point` and `code unit`?

- `A code point` is the atomic unit of information. `Text` is a sequence of code points. Each code point is a number which given meaning by the Unicode standard.
    
- `A code unit` is the unit of storage of a part of the encoded code point. In UTF-8 this means 8-bits, in UTF-16 this means 16-bits.


### What's the difference between `StringBuilder` and `StringBuffer`?

`StringBuffer`:

It is slightly less efficient, but it allows multiple threads to add or remove character.

`StringBuilder`

If all string editing happens in a single thread (which is usually the case), you should use it.


### ![20210506163135](https://img.fengqigang.cn//img/20210506163135.png) Why it return `NullPointerException`?

如果 **java** 程序要与 **windows** 下的 **cmd** 或者 **Linux** 下的 **Terminal** 交互， 就可以使用这个 **java Console** 类代劳. **Java** 要与 **Console** 进行交互式， 不总是能得到可用的 **java Console** 类的， 一个 JVM 是否有可用的 **Console** , 依赖于底层平台和 **JVM** 如何调用。 如果 **JVM** 是交互式命令行 (比如Window的cmd) 中启动的，并且输入输出没有重定向到另外的地方，那么就可以得到一个可用的 **Console** 实例

但当使用 **Eclipse** 等IDE运行以上代码时 **Console** 中将会为 **null**




