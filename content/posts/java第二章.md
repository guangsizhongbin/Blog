---
title: "Java第二章"
date: 2021-03-17T22:50:33+08:00
lastmod: 2021-03-17
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [java]
---

### 如何做文档注释?

以 /** 开头， 以 */

如

/**
 * @author gaungsizhongbin
 *
 */

### 在JAVA中数据类型分为哪几种?

基本数据类型

引用数据类型

![20210317221350](https://img.fengqigang.cn//img/20210317221350.png)

### **基本类型** 与 **引用类型** 有什么区别?

基本类型会涉及内存的分配

引用类型不会涉及内存的分配

### **基本类型** 包括哪几种?

数值型

- 整数类型 (byte, short, int, long)

- 浮点类型 (float, double)

字符型(char)

布尔型(boolean)

### **byte** 可表示的数据范围是多少?

*byte* 是8位大小， $- (2^8 / 2)$ ~ $(2^8 / 2) - 1$

![20210317222133](https://img.fengqigang.cn//img/20210317222133.png)

### **short** 可表示的数据范围是多少?

*short* 是16位大小, $- (2^{16} / 2)$ ~ $(2^{16} / 2) - 1$

![20210317222156](https://img.fengqigang.cn//img/20210317222156.png)

### **int** 可表示的数据的范围是多少?

*int* 是32位大小，$- (2^{32} / 2)$ ~ $(2^{32} / 2) - 1$

![20210317222348](https://img.fengqigang.cn//img/20210317222348.png)

### **long** 可表示的数据的范围是多少?

*long* 是64位大小, $- (2^{64} / 2)$ ~ $(2^{64} / 2) - 1$

![20210317222514](https://img.fengqigang.cn//img/20210317222514.png)

### **char** 可表示的数据的范围是多少, 其默认值什么?

*char* 是16位大小， 0~255, 其默认值为 `\u0000`

### 为什么在 **char** 为 16位大小， 其表示的数据范围是$0~255$, 而不是$- (2^{16} / 2)$ ~ $(2^{16} / 2) - 1$?


### 为什么在表示数据的范围时，最小负数绝对值总比最大正数多1?

### 如果要描述日期时间数字或者表示文件或内存大小时，用什么基本数据类型好?

long

### 如果要实现内容传递(IO 操作、网络编程)或者是编码转换(JSP开发中使用UTF-8编码), 用什么数据类型好?

byte

### 如果要想实现逻辑的控制，使用什么数据类型好?

boolean

### 如果要想算是中文，使用什么数据类型可以避免乱码问题?

char

### 如何避免由于编译器bug所造成的非正常性语法的编译错误?

在每一个操作中都加上一个" " 空格

![20210318221642](https://img.fengqigang.cn//img/20210318221642.png)

### 如何通过代码实现求int的最大值和最小值，并且实现超过其最大值和最小值的结果?

**Interger.Min_VALUE**

**Interger.MAX_VALUE**

```java
public class interger_text{
	public static void main(String arg[]){
		int max = Integer.MAX_VALUE; //取出最大值
		int min = Integer.MIN_VALUE; //取出最小值
		System.out.println(max);
		System.out.println(min);

		// int 变量 + int 型变量 = int 型数据
		System.out.println(max + 1);
		System.out.println(min - 1);
	}
}
```

![20210318222619](https://img.fengqigang.cn//img/20210318222619.png)

### 为了解决数据溢出的问题，想将 **int** 型的变量或常量变为 **long** 数据类型，该怎么做?

**常量**:

数字L

**变量**:

(long) 变量名称

```java
public class IntToLong{
	public static void main(String args[]){
		int max = Integer.MAX_VALUE;
		int min = Integer.MIN_VALUE;

		// int 变量 + long型常量 = long 型数据
		System.out.println(max + 1L);
		System.out.println(min - (long) 1);

		// long 变量 - int 型常量 = long 型数据
		System.out.println((long) min - 2);
	}
}
```

![20210318223719](https://img.fengqigang.cn//img/20210318223719.png)



