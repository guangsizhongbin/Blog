---
title: "Day29"
date: 2021-05-05T23:31:59+08:00
lastmod: 2021-05-05
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### 集合类的分类?

- Collection
	- List (线性表子接口)
		- **ArrayList**: 1
		- LinkedList: 2
		- Vector -> Stack
	- Queue (队列子接口)
		- Deque
		- BlockingQueue 	
	- Set (集合子接口)
		- HashSet: 2
		- LinkedHashSet: 3
		- TreeSet:　3
- Map (Key-value)
	- **HashMap**: 1
	- LinkedHashMap： 3
	- TreeMap： 3

### 如何解释一个集合类（HashMap）的特点, 要解释那些东西?

1. 这个集合类是谁的子类/接口

2. 这个集合类表示是的是一种什么数据结构


3. 这个集合类他的底层结构是什么(数组，链表，数组+链表)


4. 如果底层结构是数组，谈数组的默认初始容量，数组的扩容机制


5. 这个集合类是否有序(位序) 
有序: **添加的位置是不是可以预期的**

6. 这个集合类是否允许存储重复元素(二叉搜索树不允许有重复元素)

7. 这个集合类是否允许存储null

8. 这个集合类是否线程安全


### 为什么需要集合类？

很多情况下，我们需要对一组对象进行操作

很可能事先并不知道到底有多少对象

为了解决这个问题，**java** 就提供了集合类供我们使用

### 集合类有什么特点?

a. 只能存储引用数据类型: (集合类是个数据容器, 用了泛型，泛型只能是引用类型)

b. 可以自动地调整自己的大小: (实现了扩容机制)

![](https://img.fengqigang.cn//img/20210505173337.png)

### 数组和集合类都是容器，它们有什么不同?

a. 数组可以存储基本数据类型，集合不可以

b. 数组的长度是固定的，集合可以自动调整自己的大小

c. 数组的效率高，相对来说集合效率比较低

d. 数组没有API, 集合有丰富的API

### **Collection** 有什么特点?

1. Collection 是 Collection 集合体系的顶级接口

2. 一些 **collection** 的子实现是有序的，而另一些 **collection** 的子实现则是无序的

3. 一些 **collection** 的子实现是允许存储重复元素的，而另一些 **collection** 的子实现则是不允许存储重复元素的(==, 地址，compareble 自然排序)

4. 一些 **Collection** 的子实现是允许存储 null, 而另一些 **Collection** 的子实现是不允许存储null

### 接口存在有什么意义?

1. 实现多继承

2. 提供 规范 和 约束



