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

```java
public class score{
	public static void main(String args[])
	{

		int score = 100;

		// 获取十位数
		int tens = (score % 100 - score % 10) / 10;


		switch (tens){
			case  1,2,3,4,5: {
				System.out.println("不及格");
				break;
			}
			case 6: {
				System.out.println("及格");
				break;
			}
			case 7: {
				System.out.println("中");
				break;
			}
			case 8:{
				System.out.println("良");
			}
			case 9, 0:{
			
				System.out.println("优");
			}
	}
}
}
```

![20210227072502](https://img.fengqigang.cn//img/20210227072502.png)

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

```java
import java.lang.Math;

public class prime{
	public static void main(String args[]){

		boolean	flag = false;

		for (int num = 101; num <= 200; num++){
			flag = false;

			for (int a = 2; a <= Math.sqrt(num); a++){


				if ( num % a == 0 ){
					flag = true;
					break;}

			}

			if ( flag == false ){System.out.println(num + "是素数");}
		}
	}
}
```

![20210228093353](https://img.fengqigang.cn//img/20210228093353.png)



## 15.简单排序

```java
public class sort{
	public static void main(String args[]){
		int a = 1;
		int b = 2;
		int c = 3;

		if ((a > b) && (a > c))	{
			if (b > c){
				System.out.println("a > b > c");
			} else {
				System.out.println("a > c > b");
			}
		}else if ((a > b) && (a < c)){
			System.out.println("c > a > b");
		}else if ((a < b) && (a < c)){
			if (b > c){
				System.out.println("b > c > a");
			} else {
				System.out.println("c > b > a");
			}
		}else if ((a < b) && (c > a)){
			if (b > c){
				System.out.println("b > c > a");
			} else {
				System.out.println("c > b > a");
			}
		}
	}
} 
```

![20210227081159](https://img.fengqigang.cn//img/20210227081159.png)


## 16.打印三角形图案

```java
public class intrangle{
	public static void main(String args[]){
		int num = (7+1)/2 -1;

		for(int i = 1; i <= 7; i++){

			if (i%2 == 0){
				System.out.println("");
				continue;
			}else{
				for(int j = num; j > 0; j--)
					System.out.print(" ");
				num-=1;
			}

			for(int k = 1; k <= i; k++){
				System.out.print("*");
			}
			System.out.println("");

		}
	}
}
```

![20210228091116](https://img.fengqigang.cn//img/20210228091116.png)

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


## 18. 求完数

```java
public class factor{
	public static void main(String args[]){

		for (int num =1; num<100; num++){
			int count = 0;

			for(int i = 1; i < num; i++)
			{
				if(num % i == 0 ){
					count += i;
				}
			}

			if (count == num){
				System.out.println(num + "是完数");
			}
		}
	}
}
```

![20210227095719](https://img.fengqigang.cn//img/20210227095719.png)


## 19. 求不重复数字

```java
public class NotRepeat{
	public static void main(String args[]){
		for (int i = 1; i <= 4; i++){
			for (int j = 1; j <=4; j++){
				for (int k = 1; k <=4; k++){
					if (i == j | i == k | j == k)
						continue;
					System.out.println(i*100 + j*10 + k);
				}
			}
		}
	}
}
```

![20210227101516](https://img.fengqigang.cn//img/20210227101516.png)

## 20. 求日期

```java
public class daysum{
	public static void main(String args[]){
		int year = 2012;
		int month = 12;
		int day = 5;
		int day_count = 0;

		int Jan = 31;
		int Feb = 28;
		int Mar = 31;
		int Apr = 30;
		int May = 31;
		int Jun = 30;
		int Jul = 31;
		int Aug = 31;
		int Sept = 30;
		int Oct = 31;
		int Nov = 30;



		if ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0)){
			System.out.println("该年是闰年");
			Feb = 29;
		}

		switch (month){
			case 1: {
								day_count = day;
								break;
			}
			case 2: {
								day_count = Jan + day;
								break;
			}
			case 3: {
								day_count = Jan + Feb + day;
								break;
			}
			case 4: {
								day_count = Jan + Feb + Mar + day;
								break;
			}
			case 5: {
								day_count = Jan + Feb + Mar + Apr + day;
								break;
			}
			case 6: {
								day_count = Jan + Feb + Mar + Apr + May + day;
								break;
			}
			case 7: {
								day_count = Jan + Feb + Mar + Apr + May + Jun + day;
								break;
			}
			case 8: {
								day_count = Jan + Feb + Mar + Apr + May + Jun + Jul + day;
								break;
			}
			case 9: {
								day_count = Jan + Feb + Mar + Apr + May + Jun + Jul + Aug + day;
								break;
			}
			case 10: {
								 day_count = Jan + Feb + Mar + Apr + May + Jun + Jul + Aug + Sept + day;
								 break;
			}
			case 11: {
								 day_count = Jan + Feb + Mar + Apr + May + Jun + Jul + Aug + Sept + Oct + day;
								 break;
			}
			case 12: {
								 day_count = Jan + Feb + Mar + Apr + May + Jun + Jul + Aug + Sept + Oct + Nov + day;
								 break;
			}
		}

		System.out.println(day_count);
	}
}
```

![20210227112417](https://img.fengqigang.cn//img/20210227112417.png)

## 21. 根据条件求数字

```java
import java.lang.Math;

public class findnum{
	public static void main(String args[]){

		for(int num = 0 ; num <= 100000 ; num ++){
			if (Math.round(Math.sqrt(Math.sqrt(num + 100)+ 268)) == num)
				System.out.println(num);
		}
	}
}
```

![20210227113938](https://img.fengqigang.cn//img/20210227113938.png)

## 22. 根据输入求输出

```java
public class rev{
	public static void main(String args[]){
		int num = 12345;
		digts(num);
	}


	public static void digts(int num){
		int first = num % 10;
		int second = (num % 100 - first) / 10;
		int third = (num % 1000 - second) / 100;
		int four = (num % 10000 - third) / 1000;
		int five = (num % 100000 - four) / 10000;

		System.out.println("原来的数:" + num);

		if(num % 10 == num){
			System.out.println("此数为一位数");
		}else if(num % 100 == num){
			System.out.println("此数为二位数");
		}else if(num % 1000 == num){
			System.out.println("此数为三位数");
		}else if(num % 10000 == num){
			System.out.println("此数为四位数");
		}else {System.out.println("此数五位数");}

		System.out.println("转换后的数:" + first + second + third + third + five );
	}
}
```

![20210301113942](https://img.fengqigang.cn//img/20210301113942.png)


## 23. 求前20项之和

```java
public class sum{
	public static void main(String args[]){

		number(20);

	}

	public static void number(int num){
		double a = 2;
		double b = 1;
		double c = a;

		double member;
		double denominator;

		double sum = 0;


		for(int i = 1; i <= num; i++){

			member = a;
			denominator = b;

			sum += a/b;


			c = a + b;
			b = a;
			a = c;

		}
		System.out.println(sum);
	}
}

```

![20210301124037](https://img.fengqigang.cn//img/20210301124037.png)

## 24. 求阶乘

```java
public class factorial{
	public static void main(String args[]){
	
		int count = 0;
		for(int i = 1; i <= 20; i++){
			count = count + sum(i);
		}

		System.out.println(count);
	}


	public static int sum(int num){
		if (num == 1){
			return 1;
		}
		return num * sum(num - 1);
	}
}
```

![20210227201331](https://img.fengqigang.cn//img/20210227201331.png)

## 25.回文数

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


## 26.求星期几

```java
public class week{
	public static void main(String args[]){
		char first_word = 'T';
		char second_word = 'u';

		weekday (first_word, second_word);

		/*
		 * Monday
		 * Tuesday
		 * Wednesday
		 * Thursday
		 * Friday
		 * Saturday
		 * Sunday
		 */

	}

	public static void weekday(char firstword, char secondword){

		switch (firstword){
			case 'M' :{
									System.out.println("星期一");
									break;
			}

			case 'T' : {
									 switch(secondword){
										 case 'u' :{
																 System.out.println("星期二");
																 break;
										 }

										 case 'h' :{
																 System.out.println("星期四");
																 break;
										 }
									 }
									 break;
			}

			case 'W' : {
									 System.out.println("星期四");
									 break;
			}

			case 'F' : {
									 System.out.println("星期五");
									 break;
			}

			case 'S' : {
									 switch(secondword){
										 case 'a' :{
																 System.out.println("星期二");
																 break;
										 }

										 case 'u' :{
																 System.out.println("星期四");
																 break;
										 }
									 }
									 break;
			}

		}
	}
}
```





## 27.求素数

```java
import java.lang.Math;

public class prime{
	public static void main(String args[]){

		boolean	flag = false;

		for (int num = 1; num <= 100; num++){
			flag = false;

			for (int a = 2; a <= Math.sqrt(num); a++){


				if ( num % a == 0 ){
					flag = true;
					break;}

			}

			if ( flag == false ){System.out.println(num + "是素数");}
		}
	}
}
```

![20210228093648](https://img.fengqigang.cn//img/20210228093648.png)


## 28.排序算法

```java
public class sort{
	public static void main(String args[]){
		int data[] = new int[]{1, 5, 3, 2, 6, 4, 7, 8, 9, 10};

		traverse(data);
		int [] sort_data = sortnum(data);
		traverse(sort_data);
	}

	public static int[] sortnum(int[] data)
	{
		int min = 0;
		int temp;

		for(int x = 0;x < data.length; x++){
			for(int y = x + 1; y < data.length; y++){
				if(data[y] < data[min])
				{
					min = y;
				}
			}
			temp = data[x];
			data[x] = data[min];
			data[min] = temp;

			min = x+1;
		}

		return data;
	}

	public static void traverse(int[] data){
		for(int x = 0; x < data.length; x++){
			System.out.print(data[x] + " ");
		}
		System.out.println();
	}

}
```



## 29.杨辉三角

```java
public class triangle{
	public static void main(String args[]){
		int a[] = {0, 1, 0};

		for(int i = 1; i < 10; i++){
			for(int y = 10 - i; y > 1; y--){
				System.out.print(" ");
			}
			traverse(a);
			a = tri(a);
		}
	}



	public static int[] tri(int[] data){
	//	int data[] = new int[] {0, 1, 0};
	
		int dataNew[] = new int[data.length + 1];
		dataNew[0] = 0;
		dataNew[dataNew.length - 1] = 0;

		for(int x = 0, y = 1; y < data.length; x++, y++){
			dataNew[y] = (data[x] + data[y]);
		}

		return dataNew;
	}

	public static void traverse(int[] data){
		for(int x = 1; x < data.length - 1; x++)
		{
			System.out.print(data[x] + " ");

		}
		System.out.println();
	}
}
```

![20210301161735](https://img.fengqigang.cn//img/20210301161735.png)


## 30.被9整除

```java
public class number3{
	public static void main(String args[]){
		int num = 81;

		if (num % 9 == 0){
			int count = 1;
			if (num/9 == 9)
			{
				count += 1;
			}

			System.out.println(num + "能被" + count + "个" + "9除净");
		}else {System.out.println(num + "不能被9整除");}
	}
}
```

![20210228102743](https://img.fengqigang.cn//img/20210228102743.png)

## 31.三个数排序

```java
public class ArrayDemo{
	public static void main(String args[]){
		int temp;

		int data[] = new int[]{1, 2, 3, 4};


		int i = 0;
		int j = data.length - 1;
		while (i < j){
			temp = data[i];
			data[i] = data[j];
			data[j] = temp;
			i+=1;
			j-=1;
		}


		for(int x = 0; x < data.length; x++){
			System.out.print(data[x] + "、");
		}
	}
}
```

![20210227203835](https://img.fengqigang.cn//img/20210227203835.png)




## 32.加密

```java
public class encry{
	public static void main(String args[]){
		int num = 1234;
		encryNum(num);

	}

	public static void encryNum(int num){
		int first = num % 10;
		int second = (num % 100 - first) / 10;
		int third = (num % 1000 - second) / 100;
		int four = (num % 10000) / 1000;

		System.out.println(first + " " + second + " " + third + " " + four);

		first = (first + 5)%10;
		second = (second + 5)%10;
		third = (third + 5)%10;
		four = (four + 5)%10;
		
		System.out.println(first + " " + second + " " + third + " " + four);


		int temp;

		temp = first;
		first = four;
		four = temp;

		temp = second;
		second = third;
		third = temp;

		System.out.println(first * 1000 + second * 100 + third * 10 + four);

	}
}
```

![20210228191922](https://img.fengqigang.cn//img/20210228191922.png)

## 33.数组排序

```java
public class reverse{
	public static void main(String args[]){
		int Array_origial[] = new int []{1, 2, 3, 5};
		Array_origial = reverseArray(Array_origial);
		traverse(Array_origial);
		
	}

	public static int[] reverseArray(int Array_origial[]){
		int temp [] = new int [Array_origial.length];

		int foot = temp.length - 1;

		for(int x = 0; x < temp.length; x++){
			temp[x] = Array_origial[foot];
			foot --;
		}

		return temp;

	}

	public static void traverse(int temp[]){
		for(int x = 0; x < temp.length; x++)
		{
			System.out.print(temp[x] + " ");
		}
	}
}
```

![20210228141053](https://img.fengqigang.cn//img/20210228141053.png)





## 34.左移右移

```java
public class selectnum{
	public static void main(String args[]){
		int num = 1234567;
		System.out.println(select(num));

	}

	public static int select(int num){
		int fourToseven = (((num % 10000000) - num % 1000) / 1000);
		return fourToseven;
	}
}

```

![20210228172839](https://img.fengqigang.cn//img/20210228172839.png)

## 35.求奇数的个数




## 36.打印星号

```java
public class asterisk{
	public static void main(String args[]){

		int data[] = {1, 2, 3, 4, 5, 6, 7};

		for(int y = 0; y < data.length; y++){
			printaster(data[y]);
		}
	}

	public static void printaster(int num){
		for(int x = 1; x <= num; x++){
			System.out.print("*");
		}
		System.out.println("");
	}
}
```

![20210301162800](https://img.fengqigang.cn//img/20210301162800.png)



## 37.最大最小交换
```
public class arrayChange{
	public static void main(String args[]){
		int Array [] = new int[] {11, 1, 0, 6, 5};
		int positionMax = findMax(Array);
		int positionMin = findMin(Array);

		int changeMax [] = changeMax(Array, positionMax);
		System.out.println("替换最大的元素后:");
		traverse(changeMax);
		int changeMin [] = changeMin(changeMax, positionMin);
		System.out.println();
		System.out.println("替换最小的元素后:");


		traverse(changeMin);
		
	}

	public static int findMax(int temp[]){
		int max = 0;
		for(int x = 1; x < temp.length; x++)
		{
			if(temp[x] > temp[max]){max = x;};
		}
		return max;
	}

	public static int findMin(int temp[]){
		int min = 0;
		for(int x = 1; x < temp.length; x++)
		{
			if(temp[x] < temp[min]){min = x;};
		}
		return min;
	}

	public static int[] changeMax(int temp[], int position){
		int tempNum = temp[0];
		temp[0] = temp[position];
		temp[position] = tempNum;
		return temp;
	}

	public static int[] changeMin(int temp[], int position){
		int tempNum = temp[temp.length - 1];
		temp[temp.length - 1] = temp[position];
		temp[position] = tempNum;
		return temp;
	}

	public static void traverse(int temp[]){
		for(int x = 0 ;x < temp.length; x++)
		{
			System.out.print(temp[x] + " ");
		}
	}
}
```

![20210228144853](https://img.fengqigang.cn//img/20210228144853.png)

## 38.输入数字求和
```java
public class numsum{
	public static void main(String args[]){
		System.out.println(num(2,5));
		}

	public static int num (int a, int b){
		if (b == 1)
			return a;
		if (b == 2)
			return a*10 + a + num(a, 1) ;
		else{return num(a, b-1)*10 + a + num(a, b - 2);}
	}
}
```

![20210228150706](https://img.fengqigang.cn//img/20210228150706.png)

## 39.求最大公约数及最小公倍数

```java
public class elimination{
	public static void main(String args[]){
		int m = 12;
		int n = 30;

		System.out.println(eli(m, n) + "是最大公约数");
		System.out.println(((m * n) / eli(m, n)) + "是最小公倍数");

	}

	public static int eli(int m, int n){
		int c = m % n;

		if (c == 0){
			return n;
		}else {return eli(n, c);}
	}

}
```


## 40.分数累加

```java
public class acc{
	public static void main(String args[]){
		int num1=2;
		int num2=3;

		System.out.println(sum(num1));
		System.out.println(sum(num2));

	}

	public static double sum(int num){
		double sum = 0;
		if (num % 2 == 0){
			for(double i = 2.0; i <= num; i+=2)
			{
				sum += (1)/i;
			}
		}else{
			for(double i = 1.0; i <= num; i+=2){
				sum += (1)/i;
			}
			}
	return sum;
	}

}
```
![20210228171922](https://img.fengqigang.cn//img/20210228171922.png)


## 41.自由落体

```java
public class rec{
	public static void main(String args[]){

		double meter = 100;
		int num = 10;

		for(int x = 1; x <= num-1; x++)
		{
			meter += high(x) * 2;
		}

		System.out.println("第10次落地时共经过了" + meter + "米");
		System.out.println("第10次反弹有" + high(10) + "米");
	}


		public static double high(int num)
		{
			if (num == 1)
				return 50;
			else {return (high( num - 1) / 2);}
		}
}
```

![20210228195427](https://img.fengqigang.cn//img/20210228195427.png)

## 42.不死神兔子
```java
public class rabbit{
	public static void main(String args[]){

		int sum = 0;


		for(int day = 1; day <= 31; day++){
			sum += count(day);
		}

		System.out.println(sum);
	}


	public static int count(int day)
	{

		if (day == 1){
			return 1;
		}else if (day == 2){
			return 1;
		}else{return count(day - 1) + count(day - 2);}
	}
}
```

![20210228200746](https://img.fengqigang.cn//img/20210228200746.png)


## 43.猴子吃桃子问题
```java
public class monkey{
	public static void main(String args[]){

	System.out.println(peach(10));
	}
	
	public static int peach(int day){
		if (day == 1){return 1;} 
		else { return peach( day - 1 ) * 2 + 1; }
	}
}
```

![20210228204413](https://img.fengqigang.cn//img/20210228204413.png)

## 44.球赛



## 45.递归求阶乘
```java
public class renum{
	public static void main(String args[]){

		System.out.println(rec(5));

	}


	public static int rec(int num)
	{
		if(num == 1)
		{
			return 1;
		}else{return rec(num - 1) * num;}
	}

}
```

![20210228213433](https://img.fengqigang.cn//img/20210228213433.png)


## 46.求岁数

```java
public class age{
	public static void main(String args[]){

		System.out.println(whatAge(5));

	}

	public static int whatAge(int people){
		if(people == 1){
			return 10;
		}
		else{
			return whatAge(people - 1) + 2;
		}


	}
}
```

![20210228214421](https://img.fengqigang.cn//img/20210228214421.png)

## 47.插入数字



## 48.移动位置

```java
public class move{
	public static void main(String args[]){

		int data[] = {1, 2, 3, 4, 5, 6, 7};
		movePosition(data);

	}

	public static void movePosition(int data[]){
		int middle;

		if(data.length % 2 == 0){

			middle = data.length / 2;
			int tmpData[] = new int[middle];

			for(int i = 0, x = middle; i < middle; i++, x++)
			{

				tmpData[i] = data[i];
				data[i] = data[x];
				data[x] = tmpData[i];
			}

		}
		else	{

			middle = (data.length - 1) / 2;
			int tmpData[] = new int[middle];

			for(int i = 0, x = middle+1; i < middle; i++, x++)
			{

				tmpData[i] = data[i];
				data[i] = data[x];
				data[x] = tmpData[i];
			}
		};

			travel(data);
	}

	public static void travel(int data[]){
		for(int j = 0; j < data.length; j++){
			System.out.print(data[j] + " ");
		}
	}
}
```



## 49.报数



## 50.猴子分桃

```java
public class monkey{
	public static void main(String args[]){

		boolean flag = false;

		for(int i = 1; i<=5000; i++)
		{
			if(peach(i, flag) == true){break;}
		}
	}

	public static boolean peach(int i, boolean flag){
		
		if((1.25 * i + 1) % 5 == 1 ){ //第一只猴子分之前
			if((1.25 * (1.25 * i + 1) + 1) % 5 == 1){ //第二只猴子分之前
				if((1.25 * (1.25 * (1.25 * i + 1) + 1) + 1) % 5 == 1){ //第三只猴子分之前
					if((1.25 * (1.25 * (1.25 * (1.25 * i + 1) + 1) + 1) + 1) % 5 == 1){ //第四只猴子分之前
						if((1.25 * (1.25 * (1.25 * (1.25 * (1.25 * i + 1) + 1) + 1) + 1)+1) % 5 == 1){ //第五只猴子分之前
							System.out.println(i);
							flag = true;
						}
						else {return flag;};
					}
						else {return flag;};
				}
						else {return flag;};
			}
						else {return flag;};
		}
		return flag;
	}
}
```

