---
title: "Java第一章"
date: 2021-03-13T21:21:35+08:00
lastmod: 2021-03-13
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [java]
---


### 如何查看当前 **java** 版本?

```
archlinux-jav status
```

![20210313211656](https://img.fengqigang.cn//img/20210313211656.png)

### 如何编写 **Hello.java**?

```java
public class Hello {
	public static void mian(String args[]){
		System.out.println("Hello World!");
	}
}
```

### public 定义的的class有什么特点?

1. 类名称必须与文件名称保持一致

2. 在一个 *.java 中只能有一个public class

### 普通的class有什么特点?

1. 类的名称可以和文件名不致， 但是生成的class定义的名称

2. 一个*.java程序中可以同时存在多个class定义，编译后会分为不同的*.class文件

### System.out.print 与 System.out.println 有什么区别?

1. System.out.print 输出后不换行

2. System.out.println 输出后换行


