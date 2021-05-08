---
title: "Day33"
date: 2021-05-08T23:40:30+08:00
lastmod: 2021-05-08
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### Queue接口的特点

1. Queue 接口是 Collection 接口的一个子接口中
2. Queue 代表/ 描述的是队列(什么是队列: 一个操作受到限制的线性表, 在添加的时候只能在一端添加，删除是在另一端删除 -> 先进先出，后进后出)
3. 有序
4. 能存储重复元素
5. 不能存储null

(poll 方法， 如果没有元素可以删除null返回， 如果允许null存储，poll方法就没办法分辨返回的null传下到底有没有元素可删除的标记，还是原本存储的null, 所以不让存null)

![](https://img.fengqigang.cn//img/20210508105934.png)

![](https://img.fengqigang.cn//img/20210508110024.png)

### API

![](https://img.fengqigang.cn//img/20210508110328.png)


### Deque 接口

1. Deque 接口是Queue接口的一个子接口
2. Deque 在Queue接口上进行了扩展: 不仅仅可以作为普通队列，还定义了双端队列，栈
3. 有序
4. 允许重复
5. 不能存储 null(LinkedList) 除外


### ArrayDeque 特点

1. ArrayDeque 是 Deque(双端队列)的一个子实现
2. 可以作为 普通队列/ 双端队列/ 栈
3. 底层数组(循环数组)
4. 默认的初始容量16， 扩容机制(扩充2倍)

如果不大于8， 直接创建一个为8的数组

5. 有序
6. 允许重复
7. 不允许存储null
8. 线程不安全
9. 我们可以在构造方法里指定底层数组长度，但是给定的数组长度并不真的是我们给定的值 ，而是一个大于我们给定值 的最小2的幂值  -> 底层数组的长度永远是2的幂值 





**取模运算**

![](https://img.fengqigang.cn//img/20210508112009.png)


![](https://img.fengqigang.cn//img/20210508114420.png)

**构造方法**

![](https://img.fengqigang.cn//img/20210508112027.png)


![](https://img.fengqigang.cn//img/20210508112131.png)


**BlockingQueue**


