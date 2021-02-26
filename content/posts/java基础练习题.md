---
title: "Java基础练习题"
date: 2021-02-26T22:24:25+08:00
lastmod: 2021-02-26
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [java]
---

## 基础概念问答
- 1. 请问Java语言是跨平台的吗？JVM是跨平台的吗？为什么？

> Java语言是跨平台的，但JVM不是跨平台的，不同的平台有不同的JVM。 
> 首先, 后缀为 `"*.java"` 的文件，经过`javac`命令编译后会生成`public class`定义类名称的`.class`文件(字节码文件)。然后, 不同平台的JVM会根据不同操作系统所提供的接口，实现`.class`文件中的功能。

例如: Hello.java所对应的程序

```java
public class Hello {
	public static void main(String args[]){
		System.out.println("Hello, World!");
	}
}
```

编译后(Hello.class):

![20210226110518](https://img.fengqigang.cn//img/20210226110518.png)

再经过linux中的`jre-openjdk`中的`jvm`执行`hello.class`使得java看起来具有跨平台的能力。

## 环境变量
- 2. 设置环境变量使QQ或者微信可以在任意平台下，通过命令行执行

`linux`平台下:

```bash
export 文件路径:$PATH
```

![20210226112101](https://img.fengqigang.cn//img/20210226112101.png)

使用永久化:

```bash
echo  "export 文件路径:$PATH" >> .zshrc 
```

![20210226112528](https://img.fengqigang.cn//img/20210226112528.png)


## 3.[入门题目] 独立编写Hello World程序，并在命令行下运行

`hello.java`

```java
public class Hello{
	public static void main(String args[]){
		System.out.println("Hello,world");
	}
}
```

![20210226113301](https://img.fengqigang.cn//img/20210226113301.png)


```java
public class hello{
	public static void main(String args[]){
		System.out.println("Hello,world");
	}
}
```

![20210226113642](https://img.fengqigang.cn//img/20210226113642.png)

## 4.进制转换

将67转换为二进制，八进制，十六进制，将0b10100101,0345,0xef转换为十进制

1. 67

将67除以2, 商33余数为1
将商33除以2, 商16余数为1
将商16除以2, 商8余数为0
将商8除以2, 商4余数为0
将商4除以2, 商2余数为0
将商2除以2, 商1余数为0
将商1除以2, 商0余数为1

则67转换为二进制为100 0011 所对应的十六进制为43
1 000 011 对应的八进制是103

2.  0b10100101

二进制:0b 1010 0101
$1*2^{7} + 1*2^{5} + 1*2^{2} 1*2^{0} = 165$

八进制:0345
$3*8^{2} + 4*8^{1} + 5*8^{0} = 229$

十六进制:0xef
$14*16^{1} + 15*16^{0} = 239$

## 5.原码反码补码

字长为8, 已知原码 0110 1010 和1100 0110, 求他们的补码，已知补码0110 1010 和1100 0110求它们的原码

正数的补码是其本身

负数的补码是在原码的基础上，符号位不变，其余各位取反后+1

0110 1010，它是正数, 其补码为其本身 0110 1010

1100 0110, 它是负数, 其补码为1011 1010

正数补码是其本身

负数补码的原码是在其被码的基础上，符号位不变，其余各位取反后+1

0110 1010,  它是正数，其原码为其本身 0110 1010

1100 0110,  它是负数，其补码为1011 1010

## 6. 基本数据类型

语句 byte b = 300; 编译能通过吗？ 如果不能，如何让它通过？转换之后其值是多少？

不能， byte 为 8 位， 考虑符号位， 它能表示$2^7$个数, 即0 ~ 127, -128 ~ (-1)

![20210226153312](https://img.fengqigang.cn//img/20210226153312.png)



![](https://img.fengqigang.cn//img/20210226183045.png)

## 7. 位运算

用位运算求一个整数的绝对值

```java
public class number {
	public static void main(String args[]){
		
		int num = -10;

		if (num>=0){
			System.out.println("其绝对值为:" + num);
		}else{
			int negativenum = ~num + 1;
			System.out.println("其绝对值为:" + negativenum);
		}
	}
}
```


![](https://img.fengqigang.cn//img/20210226194527.png)

```java
public class number {
	public static void main(String args[]){
		
		int num = -10;
		
		int absolute = num > 0? num : ~num + 1;

		System.out.println(absolute);
	}
}
```


![](https://img.fengqigang.cn//img/20210226195211.png)

## 8.逻辑运算

有三个int变量，a, b, c 假设三个变量中有两个变量的值相同，请问如何快速求出，那个和其他两个变量不同的第三个变量的值?

```java
public class diffnum{
	public static void main(String args[]){
		int a = 1;
		int b = 2;
		int c = 1;
	
		if (a == b){
			System.out.println("c是不同的那个");
		}else if(a == c){ 
			System.out.println("b是不同的那个");
		}else{
			System.out.println("a是不同的那个");
		
		}
	}
}
```

![](https://img.fengqigang.cn//img/20210226203007.png)

## 9.左移右移
```java
public class TestOdd {
	public static void main(String args[]){
		int num = 10;
		if (num %2 == 0){
			System.out.println( num + "是2的整数次幂" );
		}	else{
			System.out.println( num + "不是2的整数次幂" );
		}
	}
}
```

![](https://img.fengqigang.cn//img/20210226201349.png)

## 10.键盘录入

```java
public class WeekDay{
	public static void main(String args[]){
		int day = 1;
		switch (day) {
			case 1: {
					System.out.println("星期一");
					break;
			}
		
			case 2: {
					System.out.println("星期二");
					break;
			}

			case 3: {
					System.out.println("星期三");
					break;
			}

			case 4: {
					System.out.println("星期四");
					break;
			}

			case 5: {
					System.out.println("星期五");
					break;
			}

			case 6: {
					System.out.println("星期六");
					break;
			}

			case 7: {
					System.out.println("星期日");
					break;
			}
			default: {
					 System.out.println("没有这天");
			}
		}
	}
}
```

![](https://img.fengqigang.cn//img/20210226203855.png)

## 11.回文数

```java
public class palnum{
	public static void main(String args[]){
		int num = 12322;

		int digit = num % 10; //个位数
		int tens = (num % 100 - num % 10) / 10; //十位数
		int thou = (num % 10000 - num % 1000) / 1000; //千分位
		int ten_t = (num % 100000 - num % 10000) / 10000; //万分位

		/*
		System.out.println(digit);
		System.out.println(tens);
		System.out.println(thou);
		System.out.println(ten_t);
		*/

		if (digit == ten_t && tens == thou)
			System.out.println( num + "是回文数" );
		else System.out.println( num + "不是回文数");
	}
}
```

![](https://img.fengqigang.cn//img/20210226212134.png)

## 12.switch分支


## 13.水仙花数

```java
public class dafnum{
	public static void main(String args[]){
	
		for (int num = 100; num <= 999; num ++){
		
			int digit = num % 10; //个位数
			int tens = (num % 100 - digit) / 10; //十位数
			int hundreds = (num - (num % 100)) / 100; //百位数
			/*
			System.out.println(digit);
			System.out.println(tens);
			System.out.println(hundreds);
			*/
			if (digit * digit * digit + tens * tens * tens + hundreds * hundreds * hundreds == num){
				System.out.println( num  + "是水仙花数" );
			}
		}
	}
}
```

![](https://img.fengqigang.cn//img/20210226210646.png)


## 14.输出素数

## 15.简单排序

## 16.打印三角形图案

## 17.打印9*9乘法表

```java
public class NtimesN{
	public static void main(String args[]){
			for(int i=1;i<=9;i++){
				for(int j=1;j<=i;j++){
					System.out.print( i +  "*" +  j + "=" + ( i * j ) + "\t" );
				}
				System.out.println();
			}
			
	}
}
```

![](https://img.fengqigang.cn//img/20210226214412.png)




