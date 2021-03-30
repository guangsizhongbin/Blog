---
title: "Day1"
date: 2021-03-30T23:02:50+08:00
lastmod: 2021-03-30
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### **JDK** 与 **JRE** 有什么样的关系?

**JRE (Java Runtime Envirment)**

Java 运行时环境

**JDK(Java Development Kit)**

Java 开发者工具包

**除了JRE外，JDK还提供了Java开发者需要使用的工具,如(javac.exe, java.exe)**

### **Java** 程序的运行原理是什么样的?

![](https://img.fengqigang.cn//img/20210330211314.png)

### 给一个 **project**起名的规范是什么?

1. 全部英文小写， 不要用中文

2. 单词之间用下划线或横杠连接

如:

**student-manage**

### 如何给一个包命名?

以反转公司域名为规范

包名应该 **全部小写**

多级包名以点(.)分隔

**包名 com.baidu**

### 如何给类、接口命名?

采用大驼峰命名法

**public class TestDemo{}**

**public class PersonDemo{}**

### 如何给变量和方法命名?

采用小驼峰命名法

**int num**;

**String name**;

### 如何给常量命名?

全部用大写

多个单词之间用下划线(_)隔开

**PI**

### 什么是小鸵峰式命名法( **lower camel case** )?

多个单词组全成一个字符串

- 第一个单词首字母 **小写**
- 第二个单词开始，首字母都要大写

**myName**,  **myFirstJavaProgram**

### 什么是大驼峰式命名法(**upper camel case**)?

多个单词组合成一个字符串

- 第一个单词首字母 **大写**
- 第二个单词开始，首字母都要大写

**MyName**, **MyFirstJavaProgram**

### 如果想要一个整数的字面值常量数据类型为 **long**, 应该如何做?

需要在后缀上加l或L, **推荐L**

### 如何想要一个浮点数字面值 常量数据类型为 **float**, 应该如何做?

需要在其后缀上加f 或F, **推荐F**

### **byte**, **short**, **int**, **long**, **float**, **double**, **char**, **boolean** 分别占用几个字节的空间?

**byte**	1个字节
**short**	 2个字节
**int**		 4个字节
**long**	 8个字节

**float**	   4个字节
**double**     8个字节

**char**	2个字节

**boolean**  

JVM规范, 在内存中 **boolean** 当作 **int** 处理， 占4个字节

**boolean** 数组当成 **byte** 数组处理， 一个 **boolean** 元素占1个字节

### **float** 只有 4字节, 会比 8 字节的 **long** 小吗?

不会， **float** 与 **double** 类型中都有 E, 会使得它比 **int** 和 **long** 要大

### **float** 的有效位数是多少?

7 ~ 8 位

### **double** 的有效位数是多少?

16 ~ 17 位

### **int** 转成 **float** 类型会出现精度丢失吗?

会

**int** 的范围为 21亿出头

**float** 的有效位只有7 ~ 8位， 会出现精度丢失

![](https://img.fengqigang.cn//img/20210330215433.png)

### **long** 转成 **double** 类型会出现精度丢失吗?

会

**long** 的范围为 922 亿亿

**double** 的范围为 16 ~ 17 位

![](https://img.fengqigang.cn//img/20210330215634.png)

### **int** 转成 **double** 类型会出现精度丢失吗?

不会

**int** 的范围为 21亿出头

**double** 的范围为16 ~ 17 位，可以包括 **int** 的范围

![](https://img.fengqigang.cn//img/20210330215634.png)

### **long** 转成 **float** 类型会出现精度丢失吗?

会

**long** 的范围为 922 亿亿

**float** 的有效位数只有7~8位
![](https://img.fengqigang.cn//img/20210330215634.png)

### **int**, **long**, **float** 哪个大？

**float** 大， **float** 中有指数

![](https://img.fengqigang.cn//img/20210330220321.png) 这些问题会出现什么结果?

1. a
2. 98
3. helloa1
4. 98hello 
5. 5+555
6. 10=5+5
7. 10.0
8. 555.0

总结: 

遇到 **'a'**, 直接输出

**'a'** + 1, 这种先考虑数值相加

**'a'** + 1 + "hello", 先考虑数值相加，然后遇到 **""** 时，合并字符串

![](https://img.fengqigang.cn//img/20210330224400.png)

### 如何实现 **Scanner** 键盘录入?

1. 导包

```java
import java.util.Scanner;
```

2. 创建对象

```java
Scanner sc = new Scanner(System.in);
```

3. 接收从键盘录入的数据

```java
int x = sc.nextInt();
```

### **next()** ， **nextInt()** 等一系列方法和 **nextLine()** 有什么区别?

**next(), nextInt() 等一系列方法**

遇见 **第一个有效字符** 时，开始扫描

当遇见**第一个分隔符或结束符**时，结束扫描，获取扫描到的内容

即获取第一个扫描到的不含空格、换行符的单个字符串

**nextLine()方法**

获取一行的内容作为一个字符串被接收

该方法不会因为空格或制表符号而结束扫描

只会因车(换行)而结束扫描

### **\u0000** 与  ** ** 有什么区别?

**\u0000** 对应的是什么都没有

![](https://img.fengqigang.cn//img/20210330225632.png)

** ** 对应的是一个空格

![](https://img.fengqigang.cn//img/20210330225709.png)


