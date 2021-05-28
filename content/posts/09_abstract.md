---
title: "09_abstract"
date: 2021-04-08T16:50:57+08:00
lastmod: 2021-04-08
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### ![20210408142941](https://img.fengqigang.cn//img/20210408142941.png) 其**jvm**内存结构图是什么样的?

![20210408143109](https://img.fengqigang.cn//img/20210408143109.png)


### 对于编译而言，怎么才能保证编译不报错?

两个引用之间是父子关系

### 什么是 **instanceof** 关键字?如何使用?

引用 **instanceof** 类名，表示该引用指向的对象，是否是后面类的对象(或子类对象)

如果是就返回 **true**, 否则就返回 false

### 怎么才能保证运行时不报错?

该父类引用指向的子类对象，就是这个要强制的子类的对象

否则会报 **ClassCastException** 类型转换异常的错误

### What will happen **x instance of C**, if x is **null**?

It simply returns **false**.

That makes sense: **null** refers to no object, so it certainly doesn't refer to an object of type c

![20210408144819](https://img.fengqigang.cn//img/20210408144819.png)

### 如何声明一个抽象类?

**语法**

\[访问权限修饰符\] abstract class 类名{}

![20210408160836](https://img.fengqigang.cn//img/20210408160836.png)

### Does abstract classes can be instantied?

No

If a class is declared as abstract, no objects of that class can be created.

But you can still create `object variables` of an abstract class, but such a variable must refer to an object of a nonabstract subclass.

Here `p` is a variable of the abstract type `Person` that refers to an instance of the nonabstract subclass `Student`.

```java
Person p = new Student("Vince Vu", "Economics");
```

### 抽象类一般如何命名?

用 **AbstractXxx** 来命名抽象类

![20210408161148](https://img.fengqigang.cn//img/20210408161148.png)

### 抽象类的成员变量与普通类的成员变量有区别吗?

**没有区别**

![20210408161339](https://img.fengqigang.cn//img/20210408161339.png)

### 抽象类可以允许定义成员方法吗?

可以

假设现有抽象类的子类中有一些方法的实现是可以被共用的，就可以抽取到抽象类中去共享它，去复用成员，复用代码

![20210408161503](https://img.fengqigang.cn//img/20210408161503.png)

### 可以继承复用静态方法吗?

**静态方法** 是不能被重写的，子类中同名的静态方法是独立的

### 抽象类中可以允许没有抽象方法吗?

允许

如果一个抽象类中没有抽象方法， 是没有太大的意义的

**普遍来说，抽象类中就应该有抽象方法**

### 有些程序员喜欢直接将一个类加上 **abstract** 声明，将该类变为抽象类，目的是让这个类无法创建对象，这种方式好吗? 为什么?

**不好**

因为抽象类是一个设计处于 **顶层祖先类的抽象概念** ，设计抽象类的目的不仅仅是创建对象

想让一个类无法创建对象，最好还是私有化构造方法

### 抽象方法可以用 **final** , **static**, **private** 修饰吗?

**都不可以**

1.  **private**

私有的方法可以继承但是没有权限， 就无法重写，抽象方法没有方法体，如果不重写没有任何意义，所以抽象方法显然不能是 **private**

2.  **static**

静态方法没有办法重写，所以也不能在抽象方法中

3.  **final**

**final** 方法不能被重写， 所以也不能用在抽象方法中

**总结:**

抽象方法被声明出来，就量要被重写的，所以不应该限制它的重写，而应该去鼓励它重写，所以普遍来说抽象方法的访问权限都是 **public**

### 抽象类中有没有构造方法?

抽象类中是 **有构造器** 的

抽象类自己不能用构造器，这个构造器 **给子类对象初始化用的**

### **Java** 中所有类都有构造方法吗?

**类** = 普通类 + 抽象类

它们都有构造方法

### 抽象类的子类有要求吗?(只能是抽象类或具体类)

抽旬类的子类可以是抽象类，也可以是具体类

**具体类**

只有当子类重写了，所有的继承自抽象类的方法，该子类才能被定义为具体类

**抽象类**

若抽象方法没有重写，则定义为抽象类

![20210408164715](https://img.fengqigang.cn//img/20210408164715.png)

### 抽象类可以继承吗?

可以

### 抽象类可以继承一个具体类吗?

可以

### 抽象类中可以继承一个抽象类吗?

可以

### **abstract** 只能用来修饰什么?

只能用来修饰 **class** 和 方法




