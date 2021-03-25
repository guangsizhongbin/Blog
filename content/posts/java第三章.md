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




