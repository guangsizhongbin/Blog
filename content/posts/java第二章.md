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

```java
public class LongToIntOverflow{
	public static void main(String args[]){
	long num = 2147483650L;
	int x = (int) num;
	System.out.println(x);
	}
}
```

![20210319143811](https://img.fengqigang.cn//img/20210319143811.png)

### **ava** 中的自动类型转换是如何规定的, 以 **byte** 变成 **int** 为例?

如果使用的数据变量类型为 **byte**, 

1. 如果设置的内容在 **byte** 数据范围 **之内**，就会自动帮助用户实现数据类型的转换

2. 如果设置的内容在 **byte** 数据范围 **之外** ，就会强制进行类型转换

### 默认情况下 **java** 只要是小数，其对应的默认数据类型就是 **double**, 如何实现 **double** 向 **float** 转换?

1. 使用字母 "F" 或 "f"

2. 在变量或常量前使用 "(float)" 声明

```java
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

```java
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

```java
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

值判断时用 **switch**

```java
public class GuessNum{
	public static void main(String args[]){
		int ch = 1;
		switch (ch) {
			case 2: {
								System.out.println("内容是2");
								break;
			}
			case 1: {
								System.out.println("内容是1");
								break;
			}
			case 3: {
								System.out.println("内容是3");
								break;
			}
			default: {
								 System.out.println("没有匹配内容");
								 break;
			}
		}
	}
}
```

### **JAVA** 中的 **while** 循环有哪两种?

while 循环

do...while 循环

### 如何用 **do...while** 循环实现100以内的加法?

```java
public class DoWhileToHundred{
	public static void main(String args[]){
		int sum = 0;
		int current = 1;
		do{
			sum += current;
			current++;
		} while (current <= 100);
		System.out.println(sum);
	}
}
```

![](https://img.fengqigang.cn//img/20210322195116.png)

### 如何用 while 循环实现100以内的加法?

**这个在实际开发中比较常用**

```java
public class WhileToHundred {
	public static void main(String args[]){
		int sum = 0;
		int current = 1;
		while(current <= 100){
			sum += current;
			current++;
		}
		System.out.println(sum);
	}
}
```

![20210322195556](https://img.fengqigang.cn//img/20210322195556.png)

### 在工作中什么时候用for循环和while循环？

**while** 循环: 在 **不确定循环次数** ，但是确定循环结束条件的情况下使用

**for** 循环: **确定循环次数** 的情况下使用

如:

一口口的吃饭，一直吃到饱为止，可是并不知道要吃多少口，只知道结束条件，

用 **while**

围着操场跑两圈步，已经明确知道了循环的次数，

用 **for**

### **continue** 与 **while** 有什么区别?

**continue** 会结束当前一次循环，直接进行下一次循环的操作

```java
public class ObserveContinue{
	public static void main(String args[]){
		for(int x = 0; x < 10; x++){
			if(x == 3){
				continue;
			}
			System.out.print("x = " + x + "、");
		}
	}
}
```

![20210322200851](https://img.fengqigang.cn//img/20210322200851.png)

**break** 会直接挑出最近的循环

```java
public class ObserveBreak{
	public static void main(String args[]){
		for(int x = 0; x < 10; x++){
		if(x == 3){
			break;
		}
		System.out.println("x = " + x + "、");
		}
	}
}
```

![](https://img.fengqigang.cn//img/20210322201203.png)

### 其他语言中的函数与 JAVA 中的方法有什么关系?

方法又被称为函数，

Java 中的英文单词是 **Method**

其他语言中的英文单词是 **Function**

### 如何写出一个没有参数，没有返回值的方法 **printInfo**?

方法要用 **static** 修饰

```java
public class NoReturnMethod {
	public static void main(String args[]) {
		printInfo();
		printInfo();
	}

	public static void printInfo() {
		System.out.println("*****************");
		System.out.println("* fengqigang.cn *");
		System.out.println("*****************");
	}
}
```

![20210323221425](https://img.fengqigang.cn//img/20210323221425.png)

### 在JAVA中，如何要给方法命名，其规范是什么?

第一个单词小写，之后每个单词首字母大写

如：

printInfo()

getMessage()

### 写文档注释需要注意什么?如何写出其文档注释![20210323221952](https://img.fengqigang.cn//img/20210323221952.png)?

1. 整个方法的用途
2. @param 变量的作用

![20210323222214](https://img.fengqigang.cn//img/20210323222214.png)

### 如何写出其文档注释?![20210323222504](https://img.fengqigang.cn//img/20210323222504.png) 

![20210323222652](https://img.fengqigang.cn//img/20210323222652.png)

### 在 **Java** 中, method 的 return 如何使用?

1. 方法有返回值声明，那么必须返回相应类型的数据

2. 方法没有返回值声明，可以直接编写 **return**

```java
public class NoneReturnMethod {
	public static void main (String args[]) {
		set(100);
		set(3);
		set(10);
	}
	/**
	 * 定义一个设置数据的操作方法，如果该数据为3将无法设置
	 * @param x 要设置的数据内容
	 */
	public static void set(int x) {
		if (x == 3) {
			return;
		}
		System.out.println("x =" + x);
	}
}
```


### 在 **Java** 中，什么是方法的重载?

是指 **方法名称相同** ，**参数的类型或个数不同** ，调用的时候将会按照传递的类型和个数完成不同方法全的执行

```java
public class MethodReload {
	public static void main(String args[]) {
		System.out.println("两个整型参数:" + add(10, 20));
		System.out.println("三个整型参数:" + add(10,20, 30));
		System.out.println("两个浮点型参数:" + add(10.2, 20.3));
	}

	/**
	 * 实现两个整型数字的加法计算操作
	 * @param x 操作数字一
	 * @param y 操作数字二
	 * @return 两个整型数据的加法计算结果
	 */
	public static int add(int x, int y){
		return x + y;
	}

	/**
	 * 实现三个整型数字的加法计算操作
	 * @param x 操作数字一
	 * @param y 操作数字二
	 * @param z 操作数字三
	 * @return 三个整型数据的加法计算结果
	 */
	public static int add(int x, int y, int z){
		return x + y + z;
	}

	/**
	 * 实现三个小数的加法计算操作
	 * @param x 操作数字一
	 * @param y 操作数字二
	 * @return 两个小数的加法计算结果
	 */
	public static double add(double x, double y){
		return x + y;
	}
}
```

![20210324215507](https://img.fengqigang.cn//img/20210324215507.png)

### 在设计方法重载时需要注意什么?

1. 所有重载后的方法使用同一种返回值类型

2. 根据 **参数类型及个数来区分不同的方法** ，而不是依靠返回值的不同来确定的

### 什么是递归调用?

是指方法自己调用自己形式

### 若使用递归操作需要满足什么条件?

1. 必须有结束条件

2. 第次调用时都需要改变传递的参数

![20210324220022](https://img.fengqigang.cn//img/20210324220022.png)

### 如何用递归写出1-100累加?

```java
public class RecusiveAddToHundred {
	public static void main(String args[]){
		System.out.println(sum(100));
	}
	/**
	 * 数据的累加操作
	 * @param num 要进行累加的操作
	 * @return 数据的累加结果
	 */
	public static int sum(int num){
		if (num == 1){
			return 1;
		}
		return num + sum(num - 1);
	}
}
```

