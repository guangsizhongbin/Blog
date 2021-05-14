---
title: "01_basic"
date: 2021-03-30T23:02:50+08:00
lastmod: 2021-03-30
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

[toc]

### **JDK** 与 **JRE** 有什么样的关系?

**JRE (Java Runtime Environment)**

Java 运行时环境

**JDK(Java Development Kit)**

Java 开发者工具包

**除了JRE外，JDK还提供了Java开发者需要使用的工具,如(javac.exe, java.exe)**

### **Java** 程序的运行原理是什么样的?

![](https://img.fengqigang.cn//img/20210330211314.png)

### 给一个 **project**起名的规范是什么?

1.  全部英文小写， 不要用中文
    
2.  单词之间用下划线或横杠连接
    

如:

**student-manage**

### How to absolutely guarantee a unique **package name**?

Use an Internet domain name written in reverse.

For example, consider the domain **horstmann.com**

When written in reverse order, it turns into the package name **com.horstmann**

You can then append a project name, such as **com.horstmann.corejava**

If you then place the **Employee** class into the package, the "fully qualified" name becomes **com.horstmann.corejava.Employee**

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

### 什么是小鸵峰式命名法( **lower camel case** )?

多个单词组全成一个字符串

- 第一个单词首字母 **小写**
- 第二个单词开始，首字母都要大写

**myName**, **myFirstJavaProgram**

### 什么是大驼峰式命名法(**upper camel case**)?

多个单词组合成一个字符串

- 第一个单词首字母 **大写**
- 第二个单词开始，首字母都要大写

**MyName**, **MyFirstJavaProgram**

### 如果想要一个整数的字面值常量数据类型为 **long**, 应该如何做?

需要在后缀上加l或L, **推荐L**

### 如何想要一个浮点数字面值 常量数据类型为 **float**, 应该如何做?

需要在其后缀上加f 或F, **推荐F**

### 若想表示一个 十六进制的数(Hexadecimal number), 应该如何做?

Hexadecimal number have a prefix 0x or 0X

for example

`0xCAFE`

```java
public class TestInt {
    public static void main(String[] args) {
        System.out.println(0xF);
    }
}
```

![20210503234107](https://img.fengqigang.cn//img/20210503234107.png)

### 若想表示一个8进制的数(Octual number)，应该如何做?

Octual numbers have a prefix 0

**naturally, this can be confusing, so we recommend against the use of octal constants**

for example

`010`

```java
public class TestInt {
    public static void main(String[] args) {
        System.out.println(010);
    }
}
```

![20210503234305](https://img.fengqigang.cn//img/20210503234305.png)

### 若想表示一个二进制(binary)，应该如何做?

write number in binary, with a prefix `0b` or `0B`

for example, 0b1001

```java
public class TestInt {
    public static void main(String[] args) {
        System.out.println(0b1001);
    }
}
```

![20210503234556](https://img.fengqigang.cn//img/20210503234556.png)

Also starting with Java 7, can add underscores to number literals, such as `0b1111_0100_0010_0100_0000`

```java
public class TestInt {
    public static void main(String[] args) {
        System.out.println(0b1_1000);
    }
}
```

![20210503234919](https://img.fengqigang.cn//img/20210503234919.png)

### **byte**, **short**, **int**, **long**, **float**, **double**, **char**, **boolean** 分别占用几个字节的空间?

**byte** 1个字节
**short** 2个字节
**int** 4个字节
**long** 8个字节

**float** 4个字节
**double** 8个字节

**char** 2个字节

**boolean**

JVM规范, 在内存中

若:

**boolean** 当作 **int** 处理， 占4个字节

**boolean** 数组当成 **byte** 数组处理， 一个 **boolean** 元素占1个字节

### **float** 只有 4字节, 会比 8 字节的 **long** 小吗?

不会， **float** 与 **double** 类型中都有 E, 会使得它比 **int** 和 **long** 要大

### **float** 的有效位数是多少?

7 ~ 8 位

### **double** 的有效位数是多少?

16 ~ 17 位

### ![20210505223517](https://img.fengqigang.cn//img/20210505223517.png) 这几个数据类型相互转换哪些会出现精度丢失问题?

在**int** 和 **long** 转成 **float** 和 **double** 的时候， 只有 **int** 转向 **double** 不会出现精度丢失，其它都会出现精度丢失

![20210505223928](https://img.fengqigang.cn//img/20210505223928.png)

### **int**, **long**, **float** 哪个大？

**float** 大， **float** 中有指数

![](https://img.fengqigang.cn//img/20210330220321.png) 这些问题会出现什么结果?

1.  a
2.  98
3.  helloa1
4.  98hello
5.  5+555
6.  10=5+5
7.  10.0
8.  555.0

总结:

遇到 **'a'**, 直接输出

**'a'** \+ 1, 这种先考虑数值相加

**'a'** \+ 1 + "hello", 先考虑数值相加，然后遇到 **""** 时，合并字符串

![](https://img.fengqigang.cn//img/20210330224400.png)

### What's the difference between `next()` and `nextLine()` methods from Scanner class?

`next()` can read the input only till the space.

`nextLine()` reads input includiung space between teh words (that is, it reads till the end of line `\n`

Once the input is read, `nextLine()` positions the cursor in the next line.

### **\\u0000** 与 (空格) 有什么区别?

**\\u0000** 对应的是什么都没有

![](https://img.fengqigang.cn//img/20210330225632.png)

对应的是一个空格

![](https://img.fengqigang.cn//img/20210330225709.png)

### What's the different between Strongly typed languages and weakly typed languages?

**Weakly-typed** languages make conversions between unrelated types implicitly

![20210503232749](https://img.fengqigang.cn//img/20210503232749.png)

**Strongly-typed** languages don't allow implicit conversions between types.

![20210503232728](https://img.fengqigang.cn//img/20210503232728.png)

### What's the mean of System.out.println(0x1.0p-3)?

0.125 = $2^{-3}$ can be writeen as 0x1.0p-3

In hexadecimal notation, use a `p`, not an `e`, to denote the exponent

The base of the exponent is 2, not 10.

![20210505092123](https://img.fengqigang.cn//img/20210505092123.png)

### Could I use $ to declare Java variable?

Even though `$` is a valid Java letter, you should not use it in your own code.

It is intended for names that are generated by the Java compiler and other tools.

### If I curious as to what Unicode characters are "letters" as for as Java is concerned, what can I do?

Use **isJavaIdentifierStart** and **isJavaIndentifierPart**

```java
System.out.println(Character.isJavaIdentifierPart('c'));
```

![20210505215200](https://img.fengqigang.cn//img/20210505215200.png)

### What's mean `int i, j;`?

Declare multiple variables on a single line

i, j both are integers

**Don't recommend this style, If you declare each variable separately, your programs are easier to read.**

### In Java , how can I declare declare a constant?

Use the keyword `final` to denote a constant.

It is customary to name constants in all uppercase

For example

```java
final double CM_PER_INCH = 2.54;
```

`const` is a reserved Java keyword, but it is not currently used for anything. You must use `final` for a constant.

### How can I use logical "and" operator or logical "or" operator to avoid errors?

```java
System.out.println(x != 0 && 1 / x > x + y);
```

The second part is never evaluated if x equals zero.

Thus, 1 / x is not computed if x is zero, and no divide-by-zero error can occur.

### ![20210505231215](https://img.fengqigang.cn//img/20210505231215.png)其输出的结果是什么? 为什么?

![20210505231256](https://img.fengqigang.cn//img/20210505231256.png)

int 类型在 java 中 4字节

向左， 向左移动是对 32求余后的结果

所以向左移动32位相当于没有移动

### `>>>` 符号是干什么的?

无符号右移

a `>>>` operator fills the top bits with zero, unlike `>>` which extends the sign bit into the top bits.

**There is no** `<<<` **operator**

### float 20.5 是如何存储的?

![20210506172226](https://img.fengqigang.cn//img/20210506172226.png)

| 序号  | 过程  | 解释  |
| --- | --- | --- |
| 1   | **首先符号位为0** | 正数的符号位为0<br>负数的符号位为1 |
| 2   | 其转化为二进制为<br>10100.1 | 正数除以2取余数<br>负数乘以2取整 |
| 3   | 将二进制数转化成科学计数法<br>1.01001 x 2^4 | 4为指数部分<br>1.01001 为尾数部分 |
| 4   | 将指数部分加上127, 转换成二进制, 作exponent<br>0111 1111 + 0000 0100 | 结果为<br>1000 0011 |
| 5   | 尾数部分，隐藏高位1, 低位补0<br>101001 | 结果为0100 100000000...(23)位 |

0 1000 0011 0100 1000 0000 0000 000

### Are there any class have a `main` method?

yeah

```java
public class StaticTest{
    public static void main(String[] args){

        var staff = new Employee[3];

        staff[0] = new Employee("Tom", 40000);
        staff[1] = new Employee("Tom", 60000);
        staff[2] = new Employee("Tom", 65000);

        for (Employee e : staff){
            e.setId();
            System.out.println("name=" + e.getName() + ", id=" + e.getId() + e.getSalary());
        }

        int n = Employee.getNextId();
        System.out.println("Next available id=" + n);
    }
}

class Employee{
    private static int nextId = 1;

    private String name;
    private double salary;
    private int id;

    public Employee (String n, double s){
        name = n;
        salary = s;
        id = 0;
    }

    public String getName(){
        return name;
    }

    public double getSalary(){
        return salary;
    }

    public int getId(){
        return id;
    }

    public void setId(){
        id = nextId;
        nextId++;
    }

    public static int getNextId(){
        return nextId;
    }

    public static void main(String[] args){
        var e = new Employee("Harry", 50000);
        System.out.println(e.getName() + " " + e.getSalary());
    }

}
```

![20210508234006](https://img.fengqigang.cn//img/20210508234006.png)

