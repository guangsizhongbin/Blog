---
title: "02_method"
date: 2021-03-31T08:37:17+08:00
lastmod: 2021-03-31
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### 如何实现 **Junit** 单元测试?

```java
@Test
public void methodName() {
}
```

**public void** 是固定格式，不可以修改，否则报错

**方法的形参列表，必须为空的**，否则会报错

单元测试的类中，不要写**main**方法

![](https://img.fengqigang.cn//img/20210330140825.png)

![](https://img.fengqigang.cn//img/20210330140918.png)

### JVM内存模型是什么样的?

Java 的开发者, 在 《Java虚拟机规范》中指出:

- **JVM** (运行时数据区)内存分为
  - JVM栈
  - 堆
  - 方法区
  - 程序计数器
  - 本地方法栈

![](https://img.fengqigang.cn//img/20210330164913.png)

### **JVM内存模型**中JVM栈(stack)中有什么样的特点?

只有栈中处于栈顶的栈帧才会生效，称这为**当前栈桢，当前方法**

### JVM内存模型中JVM堆(heap)中有什么样的特点?

所有**new**出来的东西（称之为对象）都在堆上

### 基本数据类型与引用数据类型有什么区别?

1. 存储位置(本质)

   - 基本数据类型不存在"引用"的概念，数据都是直接存储在栈上的栈帧里

   - 引用数据类型在栈帧中存储引用，引用存储的只是该引用类型在堆上对象的内存地址

2. 打印变量名内容:

   - 基本数据类型，打印变量名就是该变量具体的数值

   - 引用数据类型，打印变量名显示该引用变量堆上的内存地址

### 堆上对象和栈中变量有什么区别?

1. 从存储的类型来看:

- 堆上存储的是 **new** 出来的东西，是 **引用数据类型** 的对象

- 栈上存储的是局部变量(基本数据类型, 引用类型的引用)

2. 从默认值来看:

- 堆上的变量具有默认值

  - 整型 **(byte, short, int, long)** 默认值为 0

  - 浮点类型 **(float, double)** 默认值为 0.0

  - 字符类型 **char** 默认值为 '\u0000' 空字符

  - 布尔类型 **(boolean)** 默认值是 false

  - 引用数据类型默认值是 **null**

- **栈上变量没有默认值**，声明必须显式的初始化，否则无法使用

3. 从生命周期来看:

- 堆上的对象使用完毕后，就会变成 "垃圾"， 会等待垃圾回收器进行内存回收

- 栈上的局部变量的生命周期和栈帧保持一致

### What is Overloading?

Overloading occurs if several methods have the same name but different parameters.

For example, the `String` class has four public methods called `indexOf`. They have signatures.

```java
indexOf(int)
indexOf(int, int)
indexOf(String)
indexOf(String, int)
```

The return type is not part of the method signature.

**That is, you cannot have two methods with same names and parameter types but different return types.**



