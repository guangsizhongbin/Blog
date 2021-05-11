---
title: "Day36"
date: 2021-05-11T23:26:09+08:00
lastmod: 2021-05-11
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### set 特点

1. Set 接口是 Collection 的子接口
2. 描述的是集合这种数据结构
3. 它的一些自实现是有序的(LinkedHashSet, TreeSet) 有些子实现是无序的(HashSet)
4. 有些子实现允许存储null(LinkedHashSet, HashSet), 有些子实现不允许存储 null(TreeSet)
5. 都是不允许重复元素

### set Api

- 初始化

![](https://img.fengqigang.cn//img/20210511170809.png)

collection 是 add 方法, map 是 poll 方法

- addAll

![](https://img.fengqigang.cn//img/20210511170858.png)

- clear

![](https://img.fengqigang.cn//img/20210511170923.png)

- containsAll

![](https://img.fengqigang.cn//img/20210511170938.png)

- 

![](https://img.fengqigang.cn//img/20210511170953.png)

- iterator()

![](https://img.fengqigang.cn//img/20210511171016.png)

![](https://img.fengqigang.cn//img/20210511171032.png)

map 不能使用增强for循环, 可以用interset, 

set 可以使用增强for循环

### HashSet特点

1. HashSet 是 Set 接口一个具体子实现
2. HashSet 的底层持有一个 HashMap 对象, HashMap 的底层是一个数组 + 链表 + 红黑树结构, 所以存储到 HashSet 中的元素， 实际上都存储到 HashSet 所持有 HashMap 中作为 Key 存在
3. 由于它的底层持有的是 HashMap 对象，所以无序
4. 不允许存储重复元素： 存储的元素 hash 值一样，并且两个元素直接相等或者相 equals.
5. 允许存储 nul 元素
 
它的其它特点遵从于 HashMap, 因为底层持有的是一个 HashMap 对象，负责存储数据 
 
### HashSet 的构造方法

![](https://img.fengqigang.cn//img/20210511172550.png)

### HashSet API(方法上基本上和Collection没什么差别)

### LinkedHashSet 特点

1. LinkedHashSet 是 HashSet 的一个子类(LinkedHashSet 复用HashSet方法)
2. LinkedHashSet 底层持有一个 LinkedHashMap 对象， 它是在 hashMap结构（数组 + 链表 + 红黑树）上的增强， 多维护了一个双向链表
3. LinkedHashSet 存储的元素是有序的(通过底层的双向链表保证有序)
4. LinkedHashSet 不允许存储重复的元素
5. LinkedHashSet 允许存储null

其它特点遵照于 HashSet -> HashMap

### LinkedHashSet 构造方法

![](https://img.fengqigang.cn//img/20210511173253.png)


### TreeSet 的特点

1. TreeSet 是 Set 接口一个子类，描述的数据结构 是一个红黑树

2. TreeSet 底层持有一个 TreeMap 对象， 这个TreeMap 对象的底层是红黑树

3. 大小有序

4. 不允许存储重复元素(比较大小的重复)

5. 不允许存储 null, 因为 null 没有办法比较大小

6. 线程不安全

7. 若同时实现comparable + comparator ， 会使用comparator 的比较方法

### TreeSet 构造方法

![](https://img.fengqigang.cn//img/20210511174031.png)

TreeSet 实现比较器

![](https://img.fengqigang.cn//img/20210511174232.png)


### Api

- ceiling

![](https://img.fengqigang.cn//img/20210511174635.png)

- descendingIterator

![](https://img.fengqigang.cn//img/20210511174745.png)

- descendingset

![](https://img.fengqigang.cn//img/20210511174835.png)

- first()

![](https://img.fengqigang.cn//img/20210511174845.png)

- floor(E e)

![](https://img.fengqigang.cn//img/20210511174925.png)

- headset

![](https://img.fengqigang.cn//img/20210511175015.png)

![](https://img.fengqigang.cn//img/20210511175023.png)

- last




- lower

- subSet 

![](https://img.fengqigang.cn//img/20210511175143.png)










