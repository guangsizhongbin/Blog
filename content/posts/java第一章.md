---
title: "Java第一章"
date: 2021-03-13T21:21:35+08:00
lastmod: 2021-03-13
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [java]
---

### 如何查看当前 **java** 版本?

```
archlinux-jav status
```

![20210313211656](https://img.fengqigang.cn//img/20210313211656.png)

### 如何编写 **Hello.java**?

```java
public class Hello {
	public static void mian(String args[]){
		System.out.println("Hello World!");
	}
}
```

### public 定义的的class有什么特点?

1. 类名称必须与文件名称保持一致

2. 在一个 *.java 中只能有一个public class

### 普通的class有什么特点?

1. 类的名称可以和文件名不致， 但是生成的class定义的名称

2. 一个*.java程序中可以同时存在多个class定义，编译后会分为不同的*.class文件

### System.out.print 与 System.out.println 有什么区别?

1. System.out.print 输出后不换行

2. System.out.println 输出后换行

### 类的命名规范是什么样的?

每一个单词的开关首字母大写

**TestDemo**

### **CLASSPATH** 与 **JVM** 有什么关系?

而 **JVM** 在运行的时候，需要通过 **CLASSPATH** 加载所需要的类

**CLASSPATH** 是指类的运行路径, 默认情况下 **CLASSPATH** 指向当前目录

### **PATH** 与 **CLASSPATH** 的区别是什么?

**PATH** 是操作系统的环境属性，指的是可以执行命令的程序路径。

**CLASSPATH** 是所有 *.class 文件的执行路径， Java 命令执行时将利用此路径加载所需要的 *.class 文件.

### Java 源程序文件的后缀和 Java字节码文件的后缀 分别是什么?

源程序文件: *.java

字节码文件: *.class

### Java Application 与 Java Applet 程序有什么区别?

**Java Applet** 主要是在网页中嵌入的 Java 程序

**Application** 是指有 main 方法的程序


