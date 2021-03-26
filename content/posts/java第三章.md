---
title: "Java第三章"
date: 2021-03-25T22:54:33+08:00
lastmod: 2021-03-25
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [java]
---

### 什么是类? 什么是对象?

**类**:

表示一个客观世界中某类群体的一些基本特征抽象

如:

汽车， 轮船，书

**对象**:

一个个具体的事物

如:

张三同学， 李四账户， 王五的汽车

![](https://img.fengqigang.cn//img/20210325222315.png)

总结:

**类** 实际上是对象操作的 **模板** ，但是类不能够直接使用，必须通过 **实例对象** 来使用

### 如何定义一个类为 **Book**, 并提供一个方法, 输出图书的名称和价格?

```java
class Book {
	String title;
	double price;
	/*
	 * 输出对象完整信息
	 */
	public void getInfo() { 
		System.out.println("图书名称:" + title + ", 价格:" + price);
	}
}
```

### ![](https://img.fengqigang.cn//img/20210325223421.png)如何定义一个Book类为bk, bk的title为 Java 开发， bk的price为89.9?

```java
class Book {
	String title;
	double price;
	/*
	 * 输出对象完整信息
	 */
	public void getInfo() { 
		System.out.println("图书名称:" + title + ", 价格:" + price);
	}
}

public class ClassBook {
	public static void main(String args[]){
		Book bk = new Book();
		bk.title = "Java 开发";
		bk.price = 89.9;
	}
}
```

### ![](https://img.fengqigang.cn//img/20210325223739.png) 如何调用类中的 getInfo() 方法?

** bk.getInfo() **

![](https://img.fengqigang.cn//img/20210325223920.png)

### 在 **java** 中什么是堆内存 (heap) 和 栈内存 (stack) ?

**栈内存** :

保存的是一块对内存的空间地址

**堆内存** :

保存对象的真正数据, 都是每一个对象的属性内容

![20210325224425](https://img.fengqigang.cn//img/20210325224425.png)

### ![20210325224724](https://img.fengqigang.cn//img/20210325224724.png) 以本程序为例子，分析其堆内存与栈内存?

1. 声明并实例化对象

![20210325225319](https://img.fengqigang.cn//img/20210325225319.png)

2. 设置 **title** 属性内容

![20210325225332](https://img.fengqigang.cn//img/20210325225332.png)

3. 设置 **price** 属性内容

![20210325225345](https://img.fengqigang.cn//img/20210325225345.png)

### 所有在类中定义的属性，应该如何封装?

用 **private** 封装

### 在类中已用 **private** 封装的属性，应该如何在外部使用?

**setter** 设置内容

**getter**  取得属性内容

### ![20210326165049](https://img.fengqigang.cn//img/20210326165049.png) 定义了一个Book类， 如何给这些属性设置 **setter** 、 **getter** 操作?

![20210326165450](https://img.fengqigang.cn//img/20210326165450.png)

### ![20210326165507](https://img.fengqigang.cn//img/20210326165507.png) 若程序没有使用 **getter** 方法， 是否可以不定义?

不可以

必须定义, 不管是否使用

本程序中由于 **Book** 类提供有 **getInfo()** 方法， 所以就直接利用此方法进行内容的输出。

但是对于 **Book** 类的使用还可能出现单独取得属性的情况，所以 **getter**, **setter** 必须同时提供

![20210326165637](https://img.fengqigang.cn//img/20210326165637.png)

### 什么是构造方法?

构造方法是一种特殊的方法， 它只在  **新对象实例化** 的时候调用

其 **定义的原则** :

方法名称 与 类名称相同， 没有返回值类型声明， 同时构造方法也可以进行重载

### ![20210326171922](https://img.fengqigang.cn//img/20210326171922.png) 在对象的实例化的格式中存在构造方法的使用吗?

**存在** 

1. 类名称

规定了对象的类型，即对象可以使用哪些属性与方法，都是由类定义的

2. 对象名称

如果想使用对象，需要有一个名字，这是一个唯一的标记

3. new

开辟新的堆内存空间

4. 类名称()

调用了一个和类名称一样的方法

在 java 类中， 为了保证程序可以正常的执行，即使用户没有定义任何构造方法，也会在程序编译之后自动地为类增加一个 **没有参数**、**没有方法名称**、**类名称相同**、**没有返回值**的构造方法


### 构造方法与普通方法有什么区别呢?

**构造方法**

在实例化新对象 (new) 的时候只调用一次

**普通方法**

在实例化新对象产生之后，通过 **对象.方法** 调用多次

### ![20210326173812](https://img.fengqigang.cn//img/20210326173812.png)既然构造方法没有返回值，为什么不使用 **void** 来声明构造方法呢?

如果在构造方法上使用了 **void** , 其定义的结构与普通方法就完全一样，而 **程序的编译是依靠定义结构来解析的** ，所以不能有返回值声明。

### ![20210326181758](https://img.fengqigang.cn//img/20210326181758.png)如何用构造方法来为属性赋值?

![20210326181827](https://img.fengqigang.cn//img/20210326181827.png)

### 当一个类中的结构包含属性、构造方法、普通方法、在编写时应该采取什么样的顺序?

1. 属性 (必须封装，同时提供 **setter**, **getter**)

2. 构造方法

3. 普通方法

![20210326182404](https://img.fengqigang.cn//img/20210326182404.png)

### 在一个类中对构造方法重载时，其编写顺序，最好采取什么样的规范?

重载的方法按照参数的个数由 **多到少** ，或由 **少到多** 排列

![20210326182706](https://img.fengqigang.cn//img/20210326182706.png)

### 如何对 **Book** 实现重载? ["无参"， "有一个参数 title", "有两个参数 title, price" , ]

注意 **setter** 和 **getter** 一定要设置

**这里省略了**

![20210326190551](https://img.fengqigang.cn//img/20210326190551.png)

### 根据先编写属性，然后构造方法，最后普通方法的规则，将setter、getter放到前面对吗?![20210326190950](https://img.fengqigang.cn//img/20210326190950.png) 

不对，

**setter**, **getter** 所定义的就是普通方法，它应该放到构造方法后面

### 什么是匿名对象?

栈内存没有指向堆内存

这种开辟了堆内存空间的实例化对象，**只能使用一次**, 使用一次之后就将被GC回收

![20210326191504](https://img.fengqigang.cn//img/20210326191504.png)

### ![20210326192136](https://img.fengqigang.cn//img/20210326192136.png)如何定义一个匿名对象?

**new Book("Java开发", 69.8).getInfo();**

```java
public class ClassBook {
	public static void main(String args[]){
		new Book("Java 开发", 69.8).getInfo();
	}
}
```

### 简单 Java 类有什么基本开发要求?

1. 类名称必须存在意义， 例如: Book、 Emp;

2. 类中所有的属性必须 **private** 封装， 封装后的属性必须提供 **setter**、 **getter**;

3. 类中可以提供任意多个构造语句，但是必须保留一个 **无参构造方法**

4. 类中不允许出现任何输出语句，所有信息输出必须交给被调出处输出

5. 类中需要提供有一个取得对象完整信息的方法， 暂定为 **getInfo()**, 而且返回 **String** 型数据

### 声明并开辟数组有哪两种方法?

数据类型 数组名称 [] = new 数据类型 [长度];

数据类型 [] 数组名称 = new 数据类型 [长度];

### 如何分步完成声明数组到开辟数组?

**声明数组**:

数据类型 数组名称 [] = null;

**开辟数组**:

数组名称 = new 数据类型 [长度]


如:

int data[] = num;

data = new int [3];

### **int data[] = new int[3];** 这里的3指的是什么?

是指数组的长度为3

即

**data[0]**, **data[1]**, **data[2]**

### 如何获取数组的长度? 如 **int data[] = new int[3];**

数组名称.length

data.length
