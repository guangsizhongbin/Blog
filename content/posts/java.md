---
title: "Java"
date: 2021-01-20T14:22:51+08:00
lastmod: 2021-01-20
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [java]
---

## Java运行机制

### 高级语言的运行机制

#### 编译型

使用专门的`编译器`, 针对特定平台(操作系统)将某种高级语言源代码一次性'翻译'成可被该平台硬件执行的机器码(包括机器指令和操作数), 并包装成该平台所能识别的可执行性的程序格式。


#### 解释型

使用专门的`解释器`对源程序逐行解释成特定的机器码并立即执行的语言

## Java安装

### archlinux下安装

`sudo pacman -S jdk`

## 输出Hello World

### 编写Hello World代码

`HelloWorld.java`

```java
public class HelloWorld
{
	public static void main(String[] args)
	{
		System.out.println("Hello World!");

	}
}
```

**String** 大写

**System** 大写

### 编译

`javac -d . HelloWorld.java`

{{< admonition >}}
> 1. javac <option> <source files>

> 2. **-d <directory>**
	Specify where to place generated class files
{{< /admonition >}}

### 运行

`java HelloWorld`

## 参考

疯狂的java
