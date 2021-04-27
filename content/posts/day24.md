---
title: "Day24"
date: 2021-04-27T21:44:31+08:00
lastmod: 2021-04-27
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### 数据结构和 Java 有什么关系?

**数据结构本身和JAVA没有任何关系**

只不过AVA中有多种集合、数组、等集合性质的多对象存储结构,

有时候我们希望更便捷, 更具有逻辑性的操作这些集合或者数组数据

所以我们根据数据结构的组织方式，构建了一些特殊的JAVA集合类

用于描述了一些JAVA对象的底层数据的组成关系

JAVA的集合类底层组织数据的方式，是参照某些数据结构（逻辑、思想）来进行的

### 数据结构的种类和JAVA中的集合类别有哪些？

数据结构：抽象概念/逻辑概念

**集合**：一堆数据

**线性表**：有序的序列（操作受限的线性表：栈：先进后出队列：先进先出）

Y= ax + b

**树**：一对多的数据关系，国家，族谱

**图**：多对多的关系：理论层级

### 为什么需要集合类？

很多情况下，我们需要对一组对象进行操作。而且很可能事先并不知道到底有多少个对象。为了解决这个问题，Java就提供了集合类供我们使用。

（存储更多类型问题，扩容问题, 内存空间浪费问题,数据查找问题，数据删除问题等等

### 数组的主要特点是什么?

数组是连续存储 -\> **随机访问的**

### 为什么数组的索引一般都是从0开始的呢?

**第一个层面:**

历史遗留问题, 在计算资源缺乏的过去，o标号的写法可以节省编译时间

**第二个层面:**

方便计算

**计算公式** = (下标 \- 1) * 单个元素空间 + 基础位置

### 为什么数组的效率比链表高?

**链表:**

链表是非连续存储的

**数组:**

是连续存储的

### Java 中的一维， 多维数组的内存空间是连续的吗？

在 **java** 中只有一维数组的内存空间是连续的，多维数组的内存空间不一定连续.

### 数组的基本操作(添加, 删除)的(最好情况，最坏情况，平均情况)时间复杂度?

**添加(保证元素的顺序)**

最好情况: O(1)

最坏情况: 移动n个元素

平均情况: 移动 n/2 个元素

**删除(保证元素的顺序)**

最好情况： O(1)

最坏情况: 移动 n-1 个元素, O(n)

平均情况：移动 (n-1) / 2 元素， O(n)

### 数组的查找的(根据索引查找元素，查找数组中特定值相等的元素\[大小无序，大小有序\])时间复杂度?

根据索引查找元素: O(1) 下标

查找数组中与特定值相等的元素:

1.  大小无序: O(n)
    
2.  大小有序: O($$log_2^{n}$$)
    

![](https://img.fengqigang.cn//img/20210427163104.png)

### 数组适用于什么样的情况下使用， 不适用于什么样的情况?

查找时使用: 尤其根据下标查找 -\> 大小有序的折半查找

**不适用于添加与删除, 比较慢**

### 在 **Java** 什么是链表?

一个对象持有另一个对象的引用，另一个对象持有之后的一个对象的引用... 构成链表

**java** 的角度链表的本质： 是 java 对象的相互持有和引用

![](https://img.fengqigang.cn//img/20210427163924.png)

### 链表是如何分类的?

单链表

循环单链表

双向链表

双向循环链表

### 什么是单链表?

在链表中的每一个节点，都有一个子结点，(尾结点没有子结点)

![](https://img.fengqigang.cn//img/20210427201636.png)

### 什么是循环单链表?

单链表的改进，让单链表的尾结点的下一个结点，指向头结点

![](https://img.fengqigang.cn//img/20210427201739.png)

### 什么是双向链表?

双向链表也是单链表的改进，让结点不仅可以指向之后的元素，也可以指向之前的元素

![](https://img.fengqigang.cn//img/20210427201859.png)

### 什么是双向循环链表?

双向链表的一个改进，头元素的之前指向尾元素，尾元素的之后指向头元素

![](https://img.fengqigang.cn//img/20210427202039.png)

### 如何实现单链表增加(头部， 尾部， 非头尾位置)? ![](https://img.fengqigang.cn//img/20210427202836.png)

**头部**

```java
Node node = new Node(str, top);
top = node;
```

![](https://img.fengqigang.cn//img/20210427203020.png)

**尾部**

```java
mid.next = new Node(str, null);
```

![](https://img.fengqigang.cn//img/20210427203128.png)

**非头尾位置**

```java
Node node = new Node(str, mid.next);
mid.next = nod;
```

![](https://img.fengqigang.cn//img/20210427203252.png)

### 如何实现单链表删除(头部， 尾部， 非头尾位置)? ![](https://img.fengqigang.cn//img/20210427202836.png)

**删除头结点**

```java
top = top.next;
```

![](https://img.fengqigang.cn//img/20210427203433.png)

**删除尾结点**

```java
mid.next = null;
```

![](https://img.fengqigang.cn//img/20210427203516.png)

**删除某个中间元素**

```java
mid.next = mid.next.next;
```

![](https://img.fengqigang.cn//img/20210427203648.png)

### 如何实现双链表增加(头部， 尾部， 非头尾位置)?![](https://img.fengqigang.cn//img/20210427204042.png)

**增加头元素**

```java
Node node = new Node(null, str, head);
head.pre = node;
head = node;
```

**添加尾元素**

```java
Node node = new Node(end, str, null);
end.next = node;
end = node;
```

**添加中间位置**

```java
Node node = new Node(mid, str, mid.next);
mid.next.pre = node;
mid.next = node;
```

![](https://img.fengqigang.cn//img/20210427204557.png)




###　如何实现双链表删除(头部， 尾部， 非头尾位置)?![](https://img.fengqigang.cn//img/20210427204042.png)

**删除头结点**

```java
head = head.next;
head.pre = null;
```

**删除尾结点**

```java
end = end.pre;
end.next = null;
```

**删除中间结点**

```java
mid.next.pre = mid.pre;
mid.pre.next = mid.next;
```

![](https://img.fengqigang.cn//img/20210427204825.png)


### 双向链表和单链表的时间复杂度是一样的，那为什么在工程上，我们用的一般是双向连个而不是单链表呢?

在实际工作中，根据下标查找这个操作相对添加和删除比较频繁

双向链表根据下标查找的效率， 是高于单链表的.

以空间换时间




