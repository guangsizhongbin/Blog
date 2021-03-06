---
title: "05_opp"
date: 2021-04-03T23:12:33+08:00
lastmod: 2021-04-03
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### 什么是显式赋值?

**直接赋值的方式**

```java
String brand = "华为"; 
```

### ![](https://img.fengqigang.cn//img/20210402135625.png) 其输出结果会是什么样?

**i** 与 **i8** 会是一样的

![](https://img.fengqigang.cn//img/20210402135717.png)

### 在相同的类中，整个程序的执行期间，类加载会执行多少次？

只加载一次

![](https://img.fengqigang.cn//img/20210402135842.png)


### 像 **String, System** 这种显然也是类，但是在 **jdk** 当中也会加载吗？

它们仍然会被加载

类加载都是懒加载，不是必用时，它不会加载

### **局部变量** 与 **成员变量** 有什么区别？

- **在类中定义的位置**

**局部变量**:
	
局部位置(包含方法，大括号之间往往都是局部位置)

**成员变量**:

成员位置(类中方法外)

- **在内存中的位置**

**局部变量**

栈帧中

**成员变量**

堆上的对象

- **生命周期不同**

**局部变量**

和方法的栈帧同生共死，方法调用，局部变量生效，方法执行完毕出栈，局部变量销毁

**成员变量**

和对象同生共死，是不确定的，但是只要是对象的引用被销毁了，这些对象中的成员变量也没有意义了

- **初始化值不同**

**局部变量**

没有默认初始化值， 必须手动初始化

**成员变量**

有默认初始值

### ![](https://img.fengqigang.cn//img/20210402141750.png) 为什么它不能打印 **age** ?

加了 **static** 的方法不属于普通成员方法，它是无法访问成员变量的

### ![](https://img.fengqigang.cn//img/20210402141915.png) 这里它输出的是 80 还是 100?

输出的是  **80**  , 它会选择离它最近的参数调用

### ![](https://img.fengqigang.cn//img/20210402142330.png) 为什么没法用 **this**?

隐含的传参 **this** 只针对于(普通)成员方法， 不加static的方法

对于加了 **static** 的方法，没有隐含的传参 **this**

### 默认提供无参构造，如果我手动写了有参构造，那么默认的无参还有吗?

当写了有参构造方法，默认的无参不再提供

**为了优良的编码习惯，新建一个类，一定要把无参构造加上**

**原因:**

1. 框架是可以自己创建对象，它可能去访问类的无参构造方法创建对象

2. 子类对象初始化时，依赖于父类的无参构造方法

### 在一个构造器中可以调用其他的构造器吗?

可以

但是一个构造器中用 **this** 调用别的构造器，这行代码一定处在第一行

![](https://img.fengqigang.cn//img/20210402152928.png)

### 类中可以用小驼峰法命名吗?

可以，但是会造成 **命名混乱**

 用大驼峰法会比较好

![](https://img.fengqigang.cn//img/20210402153112.png)

![](https://img.fengqigang.cn//img/20210402153135.png)

### **char** 的对象类是什么，如何获取其最大值?

**Character**


### 类中如果有两个相同数据类型的成员变量，能否用构造方法对它们分别赋值?

不能

### 什么是静态区，它是用来干什么的?

在 **JVM** 内存的设计当中，在方法区中开辟了一块 **单独的空间**，称之为静态区

静态区是用来存放"所有对象共享，整个类的对象都只有一份的数据"

在 **Java** 当中把存放在这个区域的成员，称之为静态成员，包括 **静态成员变量** 和 **静态成员方法**

**特点**:

这个属性不是某个对象所拥有，而是全体对象所共享

这样做 **可以节省内存空间，符合设计思想**


### 可以通过一个对象的引用去访问了一个静态的成员?

可以，但不建议这样做，最好通过 **类名.** 方式的访问


### 静态成员变量和普通成员变量有什么区别?(所属， 内存中的位置， 内存中出现的时间，调用方式 )

**所属不同**

成员变量:

对象, 同一个类的不同对象的成员变量是独立的

静态成员变量:

类, 同一个类的所有对象共享一个静态成员变量

**在内存中的位置不同**

成员变量:

堆上的对象里

静态成员变量:

方法区, jdk7 以前在方法区， jdk8之后移到了堆上去了

它们都具有默认值

**在内存中出现时间不同**

成员变量:

创建对象才出现，没有对象就没有成员变量

静态成员变量:

类加载结束就存在了

**调用方式不同**

成员变量:

对象名点, 只能通过对象访问

静态成员变量:

类名点, 但是也可以通过对象名点访问，但是不建议用对象名访问

### 静态成员 与 普通成员有什么不同? (调用方式， 有没有this传参，能不能访问普通成员，访问静态成员)

**调用方式**:

静态成员方法:   类名点调用

普通成员方法:		对象名点调用

**有没有this传参**:

静态成员方法:		没有

普通成员方法:		有

**能不能访问普通成员变量**

静态成员方法:		不能

普通成员方法:    能

**能不能访问静态成员变量**

静态成员方法:		都可以

普通成员方法:		都可以


### 什么时候用 **static** 修饰成员变量?

当要共享对象的属性时可以使用

只希望在整个创建对象过程中，这个 **属性仅有一个(不变)** ，也可以用static修饰

### **static** 修饰的成员方法有什么用?

1. 用 **static** 的方法，很好的调用，同类中直接方法名调用，不同类直接类名调用，无需创建对象

**Arrays.toString()**

2. 当不需要对象， 只需要便捷的调方法时，使用 **static** , 广泛应用于工具类，方便访问调用



