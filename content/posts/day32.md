---
title: "Day32"
date: 2021-05-08T09:20:43+08:00
lastmod: 2021-05-08
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### ArrayList的特点?

1.  ArrayList 是 List 接口的一个具体实现(线性表)
    
2.  底层是一个数组
    
3.  数组的默认长度(10)， 数组的扩容机制(1.5倍)
    
4.  有序
    
5.  允许重复元素
    
6.  允许null
    
7.  线程不安全
    

在默认的创建 ArrayList 对象的时候，如果不添加，那么构造方法并没有真正创建一个长度为10的数组，而是构建空数组

但是面试的时候，首先你要说的就是默认长度为10

### ArrayList 实战

```java
public class TestLink {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();

        list.add("zs");
        list.add("ls");
        list.add("wu");
        list.add("zs");
        list.add(null);

        System.out.println(list);

    }
}
```

![](https://img.fengqigang.cn//img/20210507154615.png)

### 构造方法

- 指定集合

### API

**add**

![](https://img.fengqigang.cn//img/20210507151805.png)

![](https://img.fengqigang.cn//img/20210507151835.png)

**arraycopy方法**

![](https://img.fengqigang.cn//img/20210507152341.png)

**addAll(Collection&lt;? extends E&gt;)**

![](https://img.fengqigang.cn//img/20210507152604.png)

![](https://img.fengqigang.cn//img/20210507152622.png)

**E get(int index)**

**lastIndexOf**

![](https://img.fengqigang.cn//img/20210507155035.png)

**set(int index, E element)**

**void trimToSize()**

效果就是把多余的数组位置(没存任何内容的) 不要了,

![](https://img.fengqigang.cn//img/20210507155415.png)

**void ensureCapacity(int minCapacity)**

变成一个大于或等于给定长度的一个数组，如有必要，增加此 ArrayList 实例的容量

list.ensureCapacity(2);

**clone()**

![](https://img.fengqigang.cn//img/20210507160546.png)

![](https://img.fengqigang.cn//img/20210507160748.png)

**clone** 浅表层复制

![](https://img.fengqigang.cn//img/20210507161111.png)

**可选操作**

可以不实现， 写成空方法即可

抛出异常

![](https://img.fengqigang.cn//img/20210507161437.png)

**get 遍历**

![](https://img.fengqigang.cn//img/20210507161648.png)

**iterator遍历**

**Arraylist源码分析**

**sublist源代码分析**

![](https://img.fengqigang.cn//img/20210507163248.png)

**不可以转换, 不是同一类型**

![](https://img.fengqigang.cn//img/20210507163514.png)

并发修改异常

![](https://img.fengqigang.cn//img/20210507164603.png)


### Vector 和 ArrayList 的区别?

### Vector 的特点?

1. Vector 是 List 的一个具体实现，代表是一个线性表

2. Vector 底层是一个数组

3. 默认的初始容量 10,  扩容机制 (**取决于我们在构造方法有没有给这个 Vector 一个大于0 的增量，如果了一个大于0的增量，扩容扩为旧长度+增量, 如果没有给一个的增量，扩为原来的二倍**)



4. 有序

5. 允许重复

6. 允许null

7. 线程安全


### 大多集合类都是 jdk1.2 时候就存在了， 但 vector 是 jdk1.0 开始的


### Vector 会在构造方法里就产生一个底层长度为 10 的数组 (ArrayList) 是第一次添加时产生的

### Stack的特点

1. Stack 是 Vector 的一个子类, （v-l-c）

2. Stack 的底层是个数组(复用父类Vector 的数组)

3. 默认长度:10， 默认扩容: 2倍（默认调用父类的无参的构造方法）

4. 表示一个栈

5. 可以存储null 和重复元素

6. 线程安全

7. 如何我们要在具体的逻辑中使用一个栈的话，优先使用 `deque`

8. 如果我们使用Stack时候，不要直接使用从vector继承的方法(不是语法不允许)， 我们只是希望stack作为一个栈存在(push , pop , peek)

### Stack 实战?

![](https://img.fengqigang.cn//img/20210507172949.png)

![](https://img.fengqigang.cn//img/20210507173210.png)

### Stack 与 Deque

![](https://img.fengqigang.cn//img/20210507173708.png)



### LinkedList

### LinkedList 特点

1. LinkedList 是 list的接口的一个子实现， 还是 Deque 接口的子实现 

2. 底层结构是一个双向链表

3. 有序

4. 允许null

5. 允许重复

6. 线程不安全

7. LinkedList 不仅仅可以作为一个线性表，还可以作为一个普通队列/ 双端队列/栈使用.










