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

1.  Queue 接口是 Collection 接口的一个子接口中
2.  Queue 代表/ 描述的是队列(什么是队列: 一个操作受到限制的线性表, 在添加的时候只能在一端添加，删除是在另一端删除 -> 先进先出，后进后出)
3.  有序
4.  能存储重复元素
5.  不能存储null

(poll) 方法， 如果没有元素可以删除,null返回， 如果允许null存储，poll方法就没办法分辨返回的null是没有元素可删除的标记，还是原本存储的null, 因些不让存null

![](https://img.fengqigang.cn//img/20210508105934.png)

![](https://img.fengqigang.cn//img/20210508110024.png)

### API

![](https://img.fengqigang.cn//img/20210508110328.png)

### Deque 接口

1.  Deque 接口是Queue接口的一个子接口
2.  Deque 在Queue接口上进行了扩展: 不仅仅可以作为普通队列，还定义了双端队列，栈
3.  有序
4.  允许重复
5.  不能存储 null(LinkedList) 除外

### ArrayDeque 特点

1.  ArrayDeque 是 Deque(双端队列)的一个子实现
2.  可以作为 普通队列/ 双端队列/ 栈
3.  底层数组(循环数组)
4.  默认的初始容量16， 扩容机制(扩充2倍)  方便取余运算

如果不大于8， 直接创建一个为8的数组

5.  有序
6.  允许重复
7.  不允许存储null
8.  线程不安全
9.  我们可以在构造方法里指定底层数组长度，但是给定的数组长度并不真的是我们给定的值 ，而是一个大于我们给定值 的最小2的幂值 -> 底层数组的长度永远是2的幂值

**取模运算**

![](https://img.fengqigang.cn//img/20210508112009.png)

![](https://img.fengqigang.cn//img/20210508114420.png)

**构造方法**

![](https://img.fengqigang.cn//img/20210508112027.png)

![](https://img.fengqigang.cn//img/20210508112131.png)

**BlockingQueue**

是接口

```java
public class DemoBlockingQueue {
    public static void main(String[] args) {
        ArrayBlockingQueue<String> queue = new ArrayBlockingQueue<String>(2);

        queue.offer("zs");
        queue.offer("ls");

        System.out.println(queue);
    }
}
```



![](https://img.fengqigang.cn//img/20210510140952.png)



阻塞队列无法实现扩容

**BlockingQueue** 方法以四种形式出现， 对于不能立即满足但可能在将来某一时刻可以满足的操作:

这四种形式的处理方式不同:

第一种是抛出异常，

第二种是返回一个特殊值 (null 或 false, 具体取决于操作),

第三种是在操作可以成功前，无限期阻塞当前线程

第四种是在放弃前只在给定的最大时间限制内阻塞

![](https://img.fengqigang.cn//img/20210510094657.png)

什么是阻塞队列?

首先是一个队列， 添加的时候如果没有位置，添加操作等待，如果在删除的时候，队列中没有数据可以删除，删除操作等待

超时等待?

```java
public class DemoBlockingQueue {
    public static void main(String[] args) throws InterruptedException {
        ArrayBlockingQueue<String> queue = new ArrayBlockingQueue<String>(2);

        queue.offer("zs");
        queue.offer("ls");

        queue.offer("wu", 10, TimeUnit.SECONDS);

        System.out.println(queue);
    }
}
```



**wu并没有加进去，因为此时queue已经满了**





|     | 抛出异常 | 特殊值 | 阻塞  | 超时  |
| --- | --- | --- | --- | --- |
| 插入  | add(e) | offer(e) | put(e) | offer(e, time, unit) |
| 移除  | remove(e) | poll() | take() | poll(time, unit) |
| 检查  | element() | peek() | 不可用 | 不可用 |



```java
public class DemoBlockingQueue {
    public static void main(String[] args) throws InterruptedException {
        ArrayBlockingQueue<String> queue = new ArrayBlockingQueue<String>(2);

        queue.offer("zs");
        queue.offer("ls");

        // 启动另外的一个线程, 来对这个阻塞队列做删除
        MyThead myThead = new MyThead();
        myThead.start();

        queue.take();
        System.out.println(queue);
    }
}

class MyThead extends Thread {
    @Override
    public void run() {

    }
}
```



![](https://img.fengqigang.cn//img/20210510141539.png)



```java
public class DemoBlockingQueue {
    public static void main(String[] args) throws InterruptedException {
        ArrayBlockingQueue<String> queue = new ArrayBlockingQueue<String>(2);

        queue.offer("zs");
        queue.offer("ls");

        // 启动另外的一个线程, 来对这个阻塞队列做删除
        MyThead myThead = new MyThead();
        myThead.start();

        queue.put("uu");
        System.out.println(queue);
    }
}

class MyThead extends Thread {
    @Override
    public void run() {

    }
}
```



![](https://img.fengqigang.cn//img/20210510141653.png)





**多线程**

![](https://img.fengqigang.cn//img/20210510100209.png)

**take + 多线程**

![](https://img.fengqigang.cn//img/20210510100407.png)

超时 \+ 多线程

![](https://img.fengqigang.cn//img/20210510100818.png)

在7秒内只要有位置就会被唤醒，然后添加

