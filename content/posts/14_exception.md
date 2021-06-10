---
title: "14_exception"
date: 2021-04-14T23:01:03+08:00
lastmod: 2021-04-14
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### 什么是异常? 

异常

程序运行时期出现了问题，出现了不正常的情况，称之为 异常

### 什么是编译出错?

编译出错

在程序的编译时期不能通过编译器的语法检查，所以报错

### 什么是异常类?

java 当中一切皆对象， 当程序产生异常， JVM 会把这个异常信息封装成一个对象(类)

类中封装着问题的名称, 产生的原因， 描述等多个属性信息存在

以及对这些信息进行操作的一系列方法

这些类通过继承层次构成了 java 的异常体系

### 异常中有什么需要注意的?

1.  异常的类和对象中只是存了异常的信息

2.  包括异常的原因，异常的种类等等

3.  何时抛出异常，怎么处理异常，不是由异常对象决定的

### java 中对异常体系是如何划分的?

- Throwable (祖先类)

    - Error

    - Exception

        - RuntimeException

        - 非RuntimeException

Throwable 是 java 一切错误和异常的父类，是继承层次中的祖先类

Error 是严重问题， 无法被解决

- Error 描述了 java 运行时虚拟机内部错误和资源耗尽错误

- 对于 Error , 程序自己是无能为力的，仅靠程序本身是无法恢复和预防

- 于是程序只能尽量安全的保存数据，然后终止程序，并通知用户去解决

### Exception 有什么分类?

- RuntimeException 运行时异常

- 非RuntimeException 编译时异常

### 如果错误产生在 main 方法中， java 是怎么处理的?

1.  当我们的代码执行到错误行数之前，代码是正常执行的

2.  当我们的代码执行到错误行数时，JVM 会终止程序的执行，抛出一个该异常信息封装成的对象

3.  将该对象中异常信息，打印到控制台上，告诉程序员发生了什么问题


### 如果错误产生在 main 方法中的另一个方法中，java 是怎么处理的?

1.  当程序执行到该方法的错误行数时， JVM 会终止程序的执行

2.  向上给方法的调用者抛出一个该异常信息封装的对象

3.  一直向上抛出，直到抛给 main 方法， main 方法最终抛给 JVM

4.  发生异常之前的语句正常执行，但是之后的语句都不执行了

### 什么是单分支的 **try...catch**, 其语法是什么?

```java
try {

可能出现异常的，正常的代码逻辑

} catch (要捕捉的异常对象){

在catch分支中处理具体类型的代码异常

}
```

### 在 **try...catch** 中 的 **catch** 如何写?

```java
public class Sort {
    public static void main(String[] args) {
        try {
            System.out.println("1111");
            System.out.println(10/0);
            System.out.println("2222");
        } catch (ArithmeticException ae){
            System.out.println("发生了算数除0异常");
        }
        System.out.println("3333");
    }
}
```

![20210414215300](https://img.fengqigang.cn//img/20210414215300.png)

**catch** 中必须是一个抛出异常类的对象声明

### **try..catch** 中代码是如何执行的?

1.  如果 **try** 当中没有异常

那么 **try** 中的代码会正常执行完毕， **catch** 也叫异常处理器，如果没有异常，那么它不会工作，既然没有异常，整个 **try...catch** 后的代码正常执行

2.  如果 **try** 当中有异常

恰好能够被 **catch** 捕获， **try** 当中发生异常之前的代码， 正常执行

异常那行代码会抛出异常，被 **catch** 捕获， 然后执行 **catch** 中的代码

因为异常被捕获和处理了， 不会再抛给 **jvm** 了，程序不会终止执行

### 在 **try ... catch** 当中可能产生几个异常?

最多产生一个异常，也可能不产生异常， 因为一旦产生异常 **try** 代码后的不执行了

### 如果在 **try ... catch** 异常没有被捕获会发生什么?

try 当中异常之前的代码仍然会正常执行，后面的不执行

但是这个异常没有被捕获，仍然抛给了 **jvm** ,终止程序打印异常信息，这个时候相当于没有 **try...catch** 异常处理

![20210414220044](https://img.fengqigang.cn//img/20210414220044.png)

### 如何采取单分支 **try...catch** 同时处理多个异常，而不依赖于父类?

语法:

catch(要捕捉的异常类型1 | 要捕捉的异常类型2 | 要捕捉的异常对象对象名... )

**try 当中最多有一个异常，对象名只有一个**

**|** 不是逻辑运算符中的或， 更不能用短路的， 它表示的是可以同时匹配

![20210414220620](https://img.fengqigang.cn//img/20210414220620.png)

### **printStackTrace()** 方法是做什么的?

```java
public class Sort {
    public static void main(String[] args) {
        try {
            System.out.println(10/0);
        } catch (ArithmeticException e) {
            e.printStackTrace();
        }
    }
}
```

打印出异常

![20210414220847](https://img.fengqigang.cn//img/20210414220847.png)

### 如何实现多分支异常?

```java
public class Sort {
    public static void main(String[] args) {
        int[] arr = new int[3];
        try {
            System.out.println(10 / 0);
            System.out.println(arr[4]);
            arr = null;
            System.out.println(arr.length);
        } catch (ArithmeticException e) {
            System.out.println("发生了除0异常");
            e.printStackTrace();
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("发生了数组越界异常");
            e.printStackTrace();
        } catch (NullPointerException e) {
            System.out.println("发生了空指针异常");
            e.printStackTrace();
        }
    }
}
```

### 如何实现 **接盘侠** ?

用其父类来接盘

```java
public class Sort {
    public static void main(String[] args) {
        int[] arr = new int[3];
        try {
            System.out.println(10 / 0);
            System.out.println(arr[4]);
            arr = null;
            System.out.println(arr.length);
        } catch (ArithmeticException e) {
            System.out.println("发生了除0异常");
            e.printStackTrace();
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("发生了数组越界异常");
            e.printStackTrace();
        } catch (NullPointerException e) {
            System.out.println("发生了空指针异常");
            e.printStackTrace();
        } catch (Exception e){
            System.out.println("我是接盘侠父类 Exception");
            e.printStackTrace();
        }
    }
}
```

![20210414221403](https://img.fengqigang.cn//img/20210414221403.png)

### ![20210414221821](https://img.fengqigang.cn//img/20210414221821.png) 若要实现处理除0异常，但是空指针和下标越界异常一起处理, 该如何做?

![20210414222010](https://img.fengqigang.cn//img/20210414222010.png)

### **thorws** 方法有什么用?

在方法声明时使用，声明该方法可能抛出的异常类型

**语法**:

方法名(形参列表) throws 异常列表{

}

1.  **thorws** 加了一个s, 表示一个复数，它可以抛出的异常列表可以是多个异常
    
2.  这个异常列表只表示可能性，表示可能会抛出这些异常，并不是真的一定抛出
    

所以 **throws** 关键字后面写异常的类名即可，不需要是一个对象

### 父子类方法重写 **throws** 异常列表的关系的总体原则是什么?

子类重写的方法不能抛出更多的异常

多态， 编译看左边， 父类方法没有异常不需要处理

结果运行起来子类的方法有抛出异常需要处理

这显然是矛盾了

### 方法抛出更多的运行时异常，叫不叫抛出更多的异常? 为什么?

不叫

意味着子类比父类抛出更多的运行时异常是没有问题的

### **throw** 关键字是干什么的?

**throw** 是一个单数， 所以它表示确定的抛出一个异常

throw + 异常对象

### 如何获取一个异常对象?

通过查看一个异常的构造方法

自定义的编译时异常: 继承Exception

自定义的运行时异常: 继承RuntimeException

### **throw** \+ 运行时异常一般是怎么用的?

表示在方法中抛出运行时异常对象

这里抛出异常后，方法要在这里终止执行了，后面的代码都不会执行了，这种效果很类似于 **return**

throw + 运行时异常对象， 用来替代 return 作为方法的返回值

![20210414224758](https://img.fengqigang.cn//img/20210414224758.png)

### 如何一个方法不知道该返回什么返回值时，应该如何处理?

用 **throw + 运行时异常** 来 替代 **return** 作为方法的返回值


