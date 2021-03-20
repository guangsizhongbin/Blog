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

### 为什么在 **char** 为 16位大小， 其表示的数据范围是$0$ ~ $255$, 而不是 - $(2^{16} / 2)$ ~ $(2^{16} / 2)$ - $1$?


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

### 如何将long num = 100, 变成int num的数据类型?

int (num)

```java
public class LongToIntP{
	public static void main(String args[]){
		long num = 1000;
		int x = int (num);
		System.out.println(x);
	}
}
```

![20210319143115](https://img.fengqigang.cn//img/20210319143115.png)

### long num = 2147483650L; 其转换成int会怎样?

**int** 是32位大小， 2147483650L已超过其数据范围

```
public class LongToIntOverflow{
	public static void main(String args[]){
	long num = 2147483650L;
	int x = (int) num;
	System.out.println(x);
	}
}
```

![20210319143811](https://img.fengqigang.cn//img/20210319143811.png)

### **Java** 中的自动类型转换是如何规定的, 以 **byte** 变成 **int** 为例?

如果使用的数据变量类型为 **byte**, 

1. 如果设置的内容在 **byte** 数据范围 **之内**，就会自动帮助用户实现数据类型的转换

2. 如果设置的内容在 **byte** 数据范围 **之外** ，就会强制进行类型转换

### 默认情况下 **java** 只要是小数，其对应的默认数据类型就是 **double**, 如何实现 **double** 向 **float** 转换?

1. 使用字母 "F" 或 "f"

2. 在变量或常量前使用 "(float)" 声明

```
public class DoubleToFloat{
	public static void main(String args[]){
	float f1 = 10.2F;
	float f2 = (float)10.2;
	System.out.println(f1 * f2);
	}
}
```

![20210319145717](https://img.fengqigang.cn//img/20210319145717.png)

### int, char, long型可以保存小数吗?

不可以， 只有 **float** 和 **double** 才可以保存小数

![20210319150204](https://img.fengqigang.cn//img/20210319150204.png)

### ![20210319150514](https://img.fengqigang.cn//img/20210319150514.png) 其计算结果有小数吗?为什么?

没有小数

因为两个 **int** 类型的变量计算后还是 **int** 类型

而 **int** 类型是不保存小数的，只有 **double** 和 **float** 类型才可以保存小数

![20210319150835](https://img.fengqigang.cn//img/20210319150835.png)

将其必成 **double** 类型，其最终的结果也会自动转换成 **double** 类型

### 大写字母范围与小写字母范围是多少？ 它们之间差了多少? 如何用代码实现 'A' 向 'a' 转换?

大写字母范围: 65 ~ 90

小写字母范围: 97 ~ 122

它们之间差了32

```java
public class aToA{
	public static void main(String args[]){
		char c = 'A';
		int num = c;
		num = num + 32;
		c = (char) num;
		System.out.println(c);
	}
}
```

![20210319152102](https://img.fengqigang.cn//img/20210319152102.png)

### char 可以与 int 型互相转换吗? 为什么?

可以

```java
public class NumberToChar {
	public static void main(String args[]){
		char c = 'A';
		int num = c;
		System.out.println(c);
		System.out.println(num);
	}
}
```

![20210319151611](https://img.fengqigang.cn//img/20210319151611.png)

### char 可以保存中文字符吗? 为什么?

可以， **java** 中， 使用了 **UNICODE** 编码，这种 **十六进制** 编码可以保存任意的文字

```
public class ChineseChar{
	public static void main(String args[]){
		char c = '王';
		int num = c;
		System.out.println(num);
	}
}
```

![20210319152535](https://img.fengqigang.cn//img/20210319152535.png)

### **java** 中可以用 0 或 1 来填充布尔型的变量内容吗?

不可以, 只可以用 **false** , **true**, 并且区分大小写

![20210319152941](https://img.fengqigang.cn//img/20210319152941.png)

![20210319153044](https://img.fengqigang.cn//img/20210319153044.png)

### 如何实现在 str = "Hello" 基础上，再加上 "World!!!"? 

**+=**

![20210319154150](https://img.fengqigang.cn//img/20210319154150.png)

![20210319154309](https://img.fengqigang.cn//img/20210319154309.png)

### 如何使用三目运算符号实现 int max 是 num A 与 num B 中最大的一个?

**数据类型 变量 = 布尔表达式 ? 满足此表达式时设置的内容 : 不满足此表达式时设置的内容**

```java
public class TernaryOperator{
	public static void main(String args[]){
		int numA = 10;
		int numB = 20;

		int max = numA > numB ? numA: numB;
		System.out.println(max);
	}
}
```

![20210319154915](https://img.fengqigang.cn//img/20210319154915.png)

### 普通(&) 与 短路(&&), 普通(|) 与 短路(||) 有什么区别?

&& 只要第一个条件 **不成立** 就不执行了

![20210319155503](https://img.fengqigang.cn//img/20210319155503.png)

|| 只要第一个条件 **成立** 就不执行了

![20210319155451](https://img.fengqigang.cn//img/20210319155451.png)


而 & 和 | 都需要全部执行完

### 如何用代码实现十进制转二进制?

### 如何更快的计算出2的3次方?

左移2位

```
public class TwoToEight {
	public static void main(String args[]){
		int x = 2;
		System.out.println(x << 2);
	}
}
```

![20210320193816](https://img.fengqigang.cn//img/20210320193816.png)

### 什么时候用 **if**? 什么时候用 **switch** ?

范围判断时用 **if**

值判断时用 **switch**

```java
public class CoreDegree {
	public static void main(String args[]){
		double score = 30.0;

		if(score < 60.0){
			System.out.println("小白的成绩");
		} else if(score >= 60 && score <= 90){
			System.out.println("成绩中等");
		} else if(score > 90 && score <= 100){
			System.out.println("成绩优秀");
		} else {
			System.out.println("不可能");
		}
	}
}
```

