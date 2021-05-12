---
title: "03_array"
date: 2021-03-31T22:56:56+08:00
lastmod: 2021-03-31
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### 可变参数的实质是什么?

是用数组作为参数

```java
public static int sum(int[] arr) {
    int sumValue = 0;
    for (int i = 0; i < arr.length; i++) {
        sumValue += arr[i];
    }
    return sumValue;
}

public static int sum(int... a) {
    return 1;
}
```

![](https://img.fengqigang.cn//img/20210331194134.png)

### How to write a function that computes the maximum of a variable double number of values?

**function** 

```java
private static double max(double... values) {
    double largest = Double.NEGATIVE_INFINITY;
    for (double v : values) if (v > largest) largest = v;
    return largest;
}
```

**test**

```java
public class FindMax {
    public static void main(String[] args) {
        System.out.println(max(10.2, 10.20, 19.90));

    }

    private static double max(double... values) {
        double largest = Double.NEGATIVE_INFINITY;
        for (double v : values) if (v > largest) largest = v;
        return largest;
    }
}
```

### 在使用可参数列表的时候，需要注意什么?

1.  尽量不要使用带有两个可变参数的方法，构成方法重载时要慎重，因为很容易会导致两个方法都不可用
    
2.  可变参数一定要在参数列表的最后一个
    

否则有可能运行不了

![](https://img.fengqigang.cn//img/20210331195511.png)

### 如何用增强型 **for** 循环遍历 **arr**数组?

```java
for (int i : arr) {
    System.out.print(i + "\t");
}
```
**此时这里的i, 相当于数组中的元素，而不是数组中的下标**


### What kind of situation that I can use The `for each` loop `for (variable : collection) statement` ?

The collection expression must be an **array** or an object of a class that **implement the Iterable interface**.

### How to copy one array an array variable into another?

`copyof`

```java
public class InputTest {
    public static void main(String[] args) {
        int[] luckyNumbers = new int[6];

        luckyNumbers[0] = 2;
        luckyNumbers[1] = 3;
        luckyNumbers[2] = 5;
        luckyNumbers[3] = 7;
        luckyNumbers[4] = 11;
        luckyNumbers[5] = 12;

        System.out.println("LuckNumbers 遍历");
        for (int num : luckyNumbers) {
            System.out.print(num + " ");
        }

        int[] copiedLuckyNumbers = Arrays.copyOf(luckyNumbers, luckyNumbers.length);

        System.out.println();
        System.out.println("copiedLuckNumbers 遍历");
        for (int num : copiedLuckyNumbers) {
            System.out.print(num + " ");
        }

        int[] copiedLuckyNumbers2 = Arrays.copyOf(luckyNumbers, 2 * luckyNumbers.length);

        System.out.println();
        System.out.println("copiedLuckNumbers2 遍历");
        for (int num : copiedLuckyNumbers2) {
            System.out.print(num + " ");
        }

        System.out.println();
        System.out.println("booleansArray 遍历");
        boolean[] booleansArray = new boolean[2];
        for (boolean bool : booleansArray) {
            System.out.print(bool + " ");
        }
    }
}
```

![20210507202736](https://img.fengqigang.cn//img/20210507202736.png)

The additional elements are filled with 0 if the array contains numbers, `false` if the array contains `booleans` values;

### How to use Command-Line Parameters?

```java
public class Message{
	public static void main(String[] args){
		if (args.length == 0 || args[0].equals("-h")){
			System.out.print("hello");
		}else if(args[0].equals("-g")){
			System.out.print("Goodbye,");
		}

		for (int i = 1 ; i< args.length; i++){
			System.out.print(" " + args[i]);
		}

			System.out.print("!");
	}
}
```

```bash
java Message -g cruel world
```

```
args[0] : "-g"
args[1] : "cruel"
args[2] : "world"
```

![20210507204410](https://img.fengqigang.cn//img/20210507204410.png)

### How can I use `for each` loop to vist this two-dimensional array?![20210507205550](https://img.fengqigang.cn//img/20210507205550.png)

```Java
for (int[] row : magicSquare) {
    for (int value : row) {
        System.out.println(value);
    }
}
```

or 

```java
System.out.println(Arrays.deepToString(magicSquare));
```

![20210507210240](https://img.fengqigang.cn//img/20210507210240.png)

### Does java have true multidimensional arrays?

Java has no multidimensional arrays at all, only one-dimensional arrays.

Multidimensional arrays are faked as "arrays of arrays"


### 二维数组如何声明？

数据类型[][] 二维数组名;

### int[] m, n[] 其是想表达什么? 

int[] m;

int[] n[];

### int[][] arr4 = new int[2][3]; 其堆空间是什么样的?

![](https://img.fengqigang.cn//img/20210402222758.png)


### 什么是值传递? 什么是引用传递？

**值传递**

实际上参数只传入了它的拷贝

方法结束后，随着方法栈帧的出栈，这个拷贝被销毁了，对原先的参数变量 **没有影响**

**引用传递**

方法的实际参数传入的就是地址，就是把它本身传入了

方法结束后，随着方法出栈帧，装地址的变量是被销毁了，原先的变量要 **受到影响**

### 如果方法重载，同时有固定参数的方法恰好对应，方法调用时会怎样做?

会优先调用固定参数的方法

### 什么是语法糖？

在实现原理不变，实现效果不变的情况下，但是可以简化程序员的操作，在底层处理数据，底层进行封装

### ![20210506170509](https://img.fengqigang.cn//img/20210506170509.png) 这个 **for** 循环会停下来吗? 为什么?

不会，double无法准确存储0.1这个数

