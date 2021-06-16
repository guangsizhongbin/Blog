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

### 如何 **catch**， 判断是否实现空接口?  ![20210415171814](https://img.fengqigang.cn//img/20210415171814.png)

```java
public class demo {
    public static void main(String[] args) {
        A a = new A();
        try {
            checkCloneable(a);
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
            System.out.println("请实现空接口!");
        }
        System.out.println("111");
    }


    private static void checkCloneable(A a) throws CloneNotSupportedException {
        if (a instanceof Cloneable) {
            System.out.println("实现了Cloneable接口，允许进行克隆操作, 程序正常执行");
        } else {
            throw new CloneNotSupportedException("没有实现Cloneable接口");
        }
    }
}

interface Cloneable {
}

class A {
}
```

![20210415172058](https://img.fengqigang.cn//img/20210415172058.png)

### 在设置年龄时大于150抛出异常"你活不了这么大", 小于0抛出异常"你还没出生吗? ![20210415173941](https://img.fengqigang.cn//img/20210415173941.png)

```java
public class demo {
    public static void main(String[] args) {
        Student s = new Student();
        s.setAge(151);

    }
}

class Student {
    public int age;

    public Student() {
    }

    public void setAge(int age) {
        if (age > 150) {
            throw new IllegalArgumentException("你活不能这么大");
        } else if (age < 0) {
            throw new IllegalArgumentException("你还没出生吗？");
        } else {
            this.age = age;
        }
    }
}
```

![20210415174031](https://img.fengqigang.cn//img/20210415174031.png)

### 编译期异常和运行期异常有什么区别?

**编译期异常**

必须要显式处理，否则编译不通过

**运行期异常**

可以不处理，也不以处理

### **throws** 和 **throw** 有什么区别?

**throws**

1. 用在方法声明后面，跟的是异常类名

2. 可以跟多个异常类名，用逗号隔开

3. 表示抛出异常，由该方法的调用者来处理

4. **throws** 表示出现异常的一种可能性，并不一定发生这些异常

**throw**

1. 用在方法体内，跟的是异常对象名

2. 只能抛出一个异常对象

3. 表示抛出异常，可以由方法体内的语句处理

4. 表示抛出了异常，执行 **throw** 则一定抛出了某种异常

### **finally** 关键字有什么用?

它一般跟着 **try...catch** 一起使用, 放在整个 **try...catch** 的后面

**作用**

1. **try** 中产生异常，并且正常捕获，**finally** 代码块正常执行，之后的代码也正常执行

2. **try** 中没有产生异常，**catch** 异常处理器不执行了，**finally** 代码块仍然正常执行，其后的代码也正常执行

3. **try** 中产生异常，但是没有正常捕获，**jvm** 会终止方法的执行， **try...catch** 之后的代码不执行了，但是 **finally** 仍然执行了

**无论try中什么情况，finally代码块都要执行**

### 当 **try** 当中有 **return** 时会出现什么情况?

1. 如果这个 **return** 在产生异常的代码后面，其实是没啥用，如果在前面，不能这么写

2. 如果 **catch** 中有 **return**, 并且 **catch** 正常执行，那么仍然会执行 **finally** 后再回去 **catch** 中 **return**

3.  **finally** 当中如果有 **return** , **finally** 还会执行

4. 如果 **finally** 和 **catch** 中都有 **return**, 咋办?

### ![20210415190444](https://img.fengqigang.cn//img/20210415190444.png) 如何不执行 **finally** 语句?

**System.exit(0)**

关掉虚拟机

```java
public class demo {
    public static void main(String[] args) {
        try {
            int[] arr = null;
            throw new ArithmeticException();
        } catch (ArithmeticException e) {
            e.printStackTrace();
        } finally {
            System.out.println("finally代码块执行了");
            System.exit(0);
            return;
        }
    }
}
```

### Can I use `finalize` method for cleanup?

Do not use the `finalize` method for cleanup.

That method was intended to be called before the garbage collector sweeps away an object.

**However, you simply cannot know when this method will be called, and it is now deprecated.**

### **final**, **finalize**, **finally** 有什么区别?

**final**

修饰符， 修饰 **class** , 方法， 变量 

类: 

不可继承类

方法:

不可重写方法

变量:

变量的值无法修改, 但是不会改变变量在内存中的位置

数据类型:

引用中的地址不变，但是引用的对象仍然可以修改

**finalize**

没用，类似析构函数

**finally**

和 **try...catch** 或者 **try** 一起使用，是一定会执行的代码块, 比起 **fialize** 释放资源，更安全更高效

### 自定义异常有哪几种?

**编译时异常**:

定义一个类， 继承 **Exception**, 就是一个编译时异常

![20210415191831](https://img.fengqigang.cn//img/20210415191831.png)

**运行时异常**:

定义一个类，继承 **RuntimeException**, 就是一个运行时异常

![20210415191840](https://img.fengqigang.cn//img/20210415191840.png)

### 怎么写自定义异常类的构造方法?

直接去调用父类构造器就可以 **super** 参数

```java
public class Demo {
    public static void main(String[] args) {
       try{
          testThrowRuntimeException();
       } catch (ARuntimeException e){
          e.printStackTrace();
           System.out.println("模拟处理");
       }

       try{
           testThrowException();
       } catch (AException e){
          e.printStackTrace();
           System.out.println("模拟处理");
       }

    }

    public static void testThrowRuntimeException() {throw new ARuntimeException("自定义的运行时异常");}

    public static void testThrowException() throws AException {
        throw new AException("自定义的编译时异常");
    }
}

class ARuntimeException extends RuntimeException {
    public ARuntimeException() {
        super();
    }

    public ARuntimeException(String message){
        super();
    }
}

class AException extends Exception {
    public AException(){
        super();
    }

    public AException(String message){
        super(message);
    }

}
```

![20210415225808](https://img.fengqigang.cn//img/20210415225808.png)

### 自定义异常有什么用?

如果直接使用 **jdk** 已有的异常， 比如 **IllegalArgumentException** 这个异常，看起来是可以实现效果的

但是如果 **try** 当中的代码， 本身也会产生这个异常 **IllegalArgumentException** ， 那么就不能区分对待，不能分别处理了

所以自定义异常可以区分自己写的代码的错误，不使用源码中已有的异常，避免混淆

