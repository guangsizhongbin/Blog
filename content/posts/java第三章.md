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

**bk.getInfo()**

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

### 在类中定义的属性，应该如何封装?

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

### 如何开辟一个3个长度的数组data, data[0] 为 10, data[1] 为20, data[2] 为 30, 并遍历出来?

```java
public class ListArray {
	public static void main(String args[]){
		int data[] = new int[3];
		data[0] = 10;
		data[1] = 20;
		data[2] = 30;
		for (int x = 0; x < data.length; x++){
			System.out.print(data[x] + "、");
		}
	}
}
```

![20210327082605](https://img.fengqigang.cn//img/20210327082605.png)

### 如何分步实现一个数组 **data[]** , **data[]** 的长度为3?

int data[] = null;

data = new int [3];

![20210327082804](https://img.fengqigang.cn//img/20210327082804.png)

### 数组的引用传递是什么原理?

```java
int data[] = new int[3];

data[0] = 10;

data[1] = 20;

data[2] = 30;

int temp[] = data;
```

![20210327083042](https://img.fengqigang.cn//img/20210327083042.png)

### 什么是数组的静态初始化的操作? 有哪些方法?(以data为例)

**简化格式**:

数据类型 数组名称 [] = {值, 值, ...};

**int data[] = {1, 2, 3, 4, 5};**

**完整格式**:

数据类型 数组名称 [] = new 数据类型 [] {值, 值, ...};

**int data[] = new int[] {1, 2, 3, 4, 5};**

### 初始化二维数组有什么方法?, (以data[3][3]为例)

**动态初始化**:

数据类型 数组名称[][] = new 数据类型[行的个数][列的个数];

int data [][] = new int[3][3];

**静态初始化**:

数据类型 数组名称[][] = new 数据类型[][] {{值, 值, 值}, {值, 值, 值}};

int data [][] = new int [][]{
	{1, 2, 3},{4, 5, 6}, {7, 8, 9}
};

### ![20210327084511](https://img.fengqigang.cn//img/20210327084511.png) 如何遍历这个二维数组?

![20210327084806](https://img.fengqigang.cn//img/20210327084806.png)

**注意y 是小于data[x].length**

### 在实际开发中推荐使用多维数组吗? 为什么?

不推荐

维数越多所描述的概念就越复杂

**在实际开发中很少的情况会涉及多维开发**

### ![20210327092041](https://img.fengqigang.cn//img/20210327092041.png)引用传递是什么原理?

![20210327092056](https://img.fengqigang.cn//img/20210327092056.png)

### ![20210327143424](https://img.fengqigang.cn//img/20210327143424.png) 如何实现由小到大排序?

![20210327145121](https://img.fengqigang.cn//img/20210327145121.png)

### ![20210327145539](https://img.fengqigang.cn//img/20210327145539.png)这是冒泡排序, 为什么out 要从 size - 1开始, out > 0?

因为 **data[in] > data[in + 1]** 表达式

所以 **out** 要从 **size - 1** 开始

一直会比较到 **data[0] > data[1]**

**out** 的最小值是1

所以 **out** 大于等于 0 都可以

### ![20210327150859](https://img.fengqigang.cn//img/20210327150859.png)如何实现冒泡排序?

```java
for (int out = size - 1; out > 0; out --){
	for (int in = 0; in < out; in ++){
		if(data[in] > data[in + 1]){
			int temp = data[in];
			data[in] = data[in + 1];
			data[in + 1] = temp:
		}
	}
}
```


### 转置一个数组有什么样的思路?

1. 定义一个 **新的数组** ，将原始数组按照 **倒序** 的方式插入到新的数组中，最后 **改变原始数组引用** ，将其 **指向新的数组空间**

特点:

代码里面会产生垃圾，而在进行程序开发的过程中应该尽可能少地产生垃圾空间，这样的思路 **并不是最合理的**

2. 尽可能的在 **一个数组** 里完成转置操作

### ![20210327154356](https://img.fengqigang.cn//img/20210327154356.png)如何采取定义一个新的数组的方法，转置数组?

```java
public class ArrayReverse {
	public static void main(String args[]){
		int data [] = new int [] {1, 2, 3, 4, 5, 6, 7, 8};
		int temp [] = new int [data.length];
		int foot = data.length - 1;

		for (int x = 0; x < temp.length; x++){
			temp[x] = data[foot];
			foot--;
		}
		data = temp;
		print(data);
	}

	public static void print(int temp[]){
		for (int x = 0; x < temp.length; x++){
			System.out.print(temp[x] + "、");
		}
		System.out.println();
	}
}
```

![20210327155016](https://img.fengqigang.cn//img/20210327155016.png)

![20210327155155](https://img.fengqigang.cn//img/20210327155155.png)

### 利用算法，只在一个数组上，完成转置操作的思路是什么样的?

**偶数**:

原始数组: 1, 2, 3, 4, 5, 6

第一次转置: **6** , 2, 3, 4, 5, **1**

第二次转置: 6, **5**, 3, 4, **2**, 1

第三次转置: 6, 5, **4**, **3** , 2, 1


**奇数**

原始数组: 1, 2, 3, 4, 5, 6, 7

第一次转置: **7**, 2, 3, 4, 5, 6, **1**

第二次转置: 7, **6**, 3, 4, 5, **2**, 1

第三次转置: 7, 6, **5**, 4, **3**, 2, 1

**不管数组的长度是奇数的个数还是偶数的个数，其转置的次数的计算方式是完全一样的**

![20210327160105](https://img.fengqigang.cn//img/20210327160105.png)

### 利用算法，只在一个数组上，完成转置操作, 其代码是如何实现的?

![20210327160105](https://img.fengqigang.cn//img/20210327160105.png)

```java
public class ArrayReverse {
	public static void main(String args[]){
		int data [] = new int [] {1, 2, 3, 4, 5, 6, 7, 8};
		reverse(data);
		print(data);
	}

	public static void reverse(int arr[]){
		int len = arr.length / 2;
		int head = 0;
		int tail = arr.length - 1;
		for (int x = 0; x < len; x ++){
			int temp = arr[head];
			arr[head] = arr[tail];
			arr[tail] = temp;
			head ++;
			tail --;
		}
	}

	public static void print(int temp[]){
		for (int x = 0; x < temp.length; x++){
			System.out.print(temp[x] + "、");
		}
		System.out.println();
	}
}
```
![20210327161146](https://img.fengqigang.cn//img/20210327161146.png)

### ![20210327161538](https://img.fengqigang.cn//img/20210327161538.png)二维数组(行与列相同)如何实现转置?

**只有当行数与列数相同的时候才可以发生数据的交换操作**

```java
public class transpose {
	public static void main(String args[]) {
		int data [][] = new int [][] {
			{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
		reverse(data);
		print(data);
	}

public static void reverse(int[][] data){
	for (int x = 0; x < data.length; x++){
		for (int y = x; y < data[x].length; y++ ){
			if (x != y) {
				int temp = data[x][y];
				data[x][y] = data[y][x];
				data[y][x] = temp;
			}
		}
	}
}

public static void print(int[][] data){
	for (int x = 0; x < data.length; x++){
		for (int y = 0; y < data[x].length; y++){
			System.out.print(data[x][y] + "、");
		}
		System.out.println();
	}
	System.out.println();
}
}
```

![20210327162739](https://img.fengqigang.cn//img/20210327162739.png)


### ![20210327162955](https://img.fengqigang.cn//img/20210327162955.png) 如何用代码实现这一步骤?


public static void arraycopy (Object src, int srcPos, Object dest, int destPos, int length)

src - the source array.

srcPos - starting position in the **source array**.

dest - the destionation array.

destPos - starting position in the destination data.

length - the number of array elements to be copied.

```java
public class ArrayCopy {
	public static void main(String args[]) {
		int dataA[] = new int[] {1, 2, 3, 4, 5, 6, 7, 8};
		int dataB[] = new int[] {11, 22, 33, 44, 55, 66, 77, 88};
		// 从第5个位置复制，复制到2的位置，复制3个
		System.arraycopy(dataA, 4, dataB, 2, 3);
		print(dataB);
	}

	public static void print(int temp[]) {
		for (int x = 0; x < temp.length; x++){
			System.out.print(temp[x] + "、");
		}
		System.out.print("");
	}
}
```

![20210327172214](https://img.fengqigang.cn//img/20210327172214.png)


### 使基本数据类型的数组按照由小到大的顺序排序的方法是什么?

**java.util.Arrays.sort(数组名称)**

### **java.util.Arrays.sort(数组名称)** 为什么缺陷?

只能对基本数据类型，如 **int[], double[], char[]** 进行排序, 不能对引用数据排序

### 如何使用 **java.util.Arrays.sort()** 对 **data** 排序, data 为{3, 6, 1, 2, 8, 0}?

```java
public class SortArray {
	public static void main(String args[]){
		int data[] = new int[] {3, 6, 1, 2, 8, 0};
		java.util.Arrays.sort(data);
		print(data);
	}
	public static void print(int temp[]){
		for (int x = 0; x < temp.length; x++){
			System.out.print(temp[x] + "、");
		}
	}
}
```

![20210327213624](https://img.fengqigang.cn//img/20210327213624.png)


### 什么是对象数组?

数组是 **引用类型**

类是 **引用类型**

对象数组表示一个引用类型里面 **嵌套其他的引用类型**

### 对象数组有哪些初始化的方式?

1. 动态初始化

类名称 对象数组名称 = new 类名称 [长度];

```java
Book books [] = new Book[3];
books[0] = new Book{"Java", 79.8};
books[1] = new Book{"JSP", 69.8};
books[2] = new Book{"Android", 89.8};
```

2. 静态初始化

类名称 对象数组名称 = new 类名称 [] {实例化对象, 实例化对象, ...};

```java
Book books[] = new Book[] {
	new Book("Java", 79.8),
	new Book("JSP", 69.8),
	new Book("Android", 89.8);
}
```

### ![20210327214533](https://img.fengqigang.cn//img/20210327214533.png)对象数组的内存关系是什么样的?

![20210327214548](https://img.fengqigang.cn//img/20210327214548.png)

### 如何采用动态初始化的方法初始化![20210327214648](https://img.fengqigang.cn//img/20210327214648.png)?


### 如何采用静态初始化的方法初始化![20210327214748](https://img.fengqigang.cn//img/20210327214748.png)?

### **String** 类有哪两种实例化的方式?

1. 为 **String** 类对象直接赋值

2. 利用构造方法实例化

### 如何采取直接赋值的方式对 **String** 类赋值 (如: 使str 为 "fengqigang.cn")？

```java
public class StringAttribute {
	public static void main(String args[]){
		String str = "fengqigang.cn";
		System.out.println(str);
	}
}
```

![20210328104128](https://img.fengqigang.cn//img/20210328104128.png)

### 如何采取构造方法实例化的方式对 **String** 类赋值 (如: 使str 为 "fengqigang.cn")？

```java
public class StringAttribute {
	public static void main(String args[]){
		String str = new String("fengqigang.cn");
		System.out.println(str);
	}
}
```

![20210328104410](https://img.fengqigang.cn//img/20210328104410.png)

### 在 **java** 中 "==" 可以应用到哪些数据类型中?

可以应用在所有数据类型中

包括基本数据类型与引用数据类型

### 如何判断 直接赋值的String 与 采用构造方法的创造相同内容的String, 它们是否相等(以hello为例)?

不相等

```java
public class StringCompare {
	public static void main(String args[]){
		String stra = "hello";
		String strb = new String("hello");

		System.out.println(stra == strb);
	}
}
```

### ![20210328105737](https://img.fengqigang.cn//img/20210328105737.png) 它两相等吗? 为什么?

相等

都是指向相同的堆内存

![20210328105818](https://img.fengqigang.cn//img/20210328105818.png)

### **==** 所比较的是什么?

首先， 在整个Java中只要引用数据类型一定会存在内存地址

"==" 可以用于所有的引用数据类型比较

**比较的并不会是内容，永远都只是地址的数值内容, 比较的是内存地址**

### 如何比较 **String** 类里面字符串的内容?

**public boolean equals(String str)**

### ![20210328110321](https://img.fengqigang.cn//img/20210328110321.png) 如何实现他们三者在字符串内容上的比较?

**equls**

![20210328110459](https://img.fengqigang.cn//img/20210328110459.png)

![20210328110527](https://img.fengqigang.cn//img/20210328110527.png)

### 在 **String** 类中 "==" 和 "equals()" 比较有什么区别?

"==" 

是 **Java** 提供的关系运算符

主要的功能进行数值相等判断，如果用在 **String** 对象上表示的是 **内存地址数值** 的方法

"equals()"

是由 **String** 提供的一个方法，此方法专门负责进行 **字符串内容** 的比较

### ![20210328144311](https://img.fengqigang.cn//img/20210328144311.png) 其结果是什么样的? 为什么?

![20210328144338](https://img.fengqigang.cn//img/20210328144338.png)

这是实现了堆内存空间的重用

即采用直接赋值的方式，在相同内容的情况下不会开辟新的内存空间 ,  而会直接指向已有的内存空间

![20210328144603](https://img.fengqigang.cn//img/20210328144603.png)

在 **JVM** 的底层实际上会存在一个 **对象池** (不一定只保存 **String** 对象) , 当代码中使用了直接赋值的方式定义一个 **String** 类对象时，会将此字符串对象所使用的匿名对象入池保存。

如果后续还有其他 **String** 类对象也采用了直接赋值的方式，并设置了同样的内容时，将不会开辟新的堆内存空间，而是使用已有的对象进行引用的分配, 从而继续使用。

### **String** 采取直接赋值的方式实例化, 其语法是什么样的(以 "hello" 为例)?

```java
String 变量 = 字符串常量(匿名对象)

String str = "hello";
```

![20210328150540](https://img.fengqigang.cn//img/20210328150540.png)


### **String** 采取构造方法的方式实例化, 其语法是什么样的(以 "hello" 为例)?

```java
String str = new String("hello");
```

### **String** 采取构造方法的方式实例化, 其特点是什么?

```java
String str = new String("hello");
```

![20210328150836](https://img.fengqigang.cn//img/20210328150836.png)


因为每一个字符串都是一个 **String** 类匿名对象

会首先在堆内存中开辟一块空间保存字符串"hello", 然后使用关键字 **new**, 开辟另一块内存空间

在真正使用的是关键字 **new** 开辟的堆内存， 而之前定义的字符串常量的堆内存空间将不会在任何的栈内存指向，将成为垃圾，等待被 **GC** 回收.

总结:

使用构造方法开辟的字符串对象，实际上会 **开辟两块空间** ，其中有 **一块空间将成为垃圾**


### **String** 类有哪两种实例化的方式?

1. 直接赋值实例化 **String** 类对象

2. 构造方法实例化 **String** 类对象

### 每一个字符串常量， 其本质上是什么? 为什么？

**String** 匿名对象

```java
public class StringAnonymity {
	public static void main(String args[]) {
		String str = "hello";
		System.out.println("hello".equals(str));
	}
}
```

![20210328150254](https://img.fengqigang.cn//img/20210328150254.png)

**"hello"** 直接调用了 **equals()** 方法

由于 **equals()**  方法是 **String** 类定义的，而类中的方法只有实例化对象才可以调用

所以字符串常量就是 **String** 类的匿名对象

### ![20210328151610](https://img.fengqigang.cn//img/20210328151610.png) 其结果是什么? 为什么?

![20210328151704](https://img.fengqigang.cn//img/20210328151704.png)

因为这种采取构造方法定义的内存空间，不会自动入池

所以在使用赋值的方式声明 **String** 类对象后将开辟新的堆内存空间，因为两个堆内存的地址不同，所以最终的地址判断结果为 **false**

### 若采取构造方法定义的新的内存空间如何手动入池?

**new String("hello").intern()**

![20210328152159](https://img.fengqigang.cn//img/20210328152159.png)

![20210328152222](https://img.fengqigang.cn//img/20210328152222.png)

### 采取 **直接赋值** (String str = "字符串";) 和 **构造方法** (String str = new String("字符串")) 实例化方式有什么区别?

**直接赋值**

只会开辟一块堆内存空间，并且会自动保存在对象池以供下次重复使用

**构造方法**

会开辟两块堆内存空间，其中一块空间将成为垃圾，并且不会自动入池，但是用户可以使用 **intern()** 方法手动入池

### ![20210328152921](https://img.fengqigang.cn//img/20210328152921.png) 其本质上是什么样的?

![20210328153010](https://img.fengqigang.cn//img/20210328153010.png)

首先，声明了一个 **String*8 类对象, 然后修改了两次 **String** 类对象的内容 (实际上是发生了两次引用改变), 所以最终 **String** 类对象的内容就是 **"Hello, World!!!"**

**只是 String 类的对象引用发生了改变，而字符串的内容并没有发生改变**


### ![20210328153626](https://img.fengqigang.cn//img/20210328153626.png) 这种操作可以做吗? 为什么?

修改 **String** 对象的值，相当于修改其引用关系，(**所有数据类型遇见String连接操作时都会自动向String类型转换**), 并且会产生大量的垃圾空间

### 因为修改 **String** 对象的值，相当于修改其引用关系，若在一个项目中要大量的修改一个字符串，该如何解决?

使用 **StringBuffer** 或 **StringBuilder**

### 如何截取指定索引的字符(如截取第一个字符)?

使用 **charAt()** 方法

charAt(0) 截取第一个字符

```java
public class CharAt {
	public static void main(String args[]) {
		String str = "hello";
		char c = str.charAt(0);
		System.out.println(c);
	}
}
```

![20210328154608](https://img.fengqigang.cn//img/20210328154608.png)

###  如何实现字符数组与字符串的转换?

**toCharArray()**

```java
public class ToCharArray {
	public static void main(String args[]) {
		String str = "hello";
		char[] data = str.toCharArray();
		for (int x = 0; x < data.length; x++){
			System.out.print(data[x] + "、");
		}
	}
}
```


