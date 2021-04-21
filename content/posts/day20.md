---
title: "Day20"
date: 2021-04-21T17:00:51+08:00
lastmod: 2021-04-21
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### 线程有哪5种状态?

**新建**: 

刚创建的线程，没有执行 start() 方法， 没有资格去挣抢CPU资源

**就绪**

刚执行了 **start** 方法， 但是还没有获得CPU的执行权

**执行**

抢到了 CPU的执行权

**阻塞**

没有 CPU 的执行权，还缺少必要的条件（sleep 结束）

**死亡**

run 方法执行完之后

### 线程5个状态之间是如何转换?

![](https://img.fengqigang.cn//img/20210421095335.png)

### 用Runnable实现多线程?

1. 实现 Runnable 接口

2. 重写 run 方法

3. 创建 Runnable 子类对象

4. 创建 Thread 对象， 并且把 Runnable 子类对象作为参数传递

5. start 方法 

```java
public class RunnableDemo {
    public static void main(String[] args) {
        MyRunnable myRunnable = new MyRunnable();
        Thread thread = new Thread(myRunnable);

        thread.start();
        for (int i = 0; i < 10; i++) {
            System.out.println(Thread.currentThread().getName() + "--------" + i);
        }

    }
}

class MyRunnable implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println(Thread.currentThread().getName() + "-------" + i);
        }
    }
}
```

### 为什么 Runnable 接口子类的 run() 方法代码， 会执行在子线程当中？

![](https://img.fengqigang.cn//img/20210421101452.png)

### Runnable 对象代表线程吗?

 不代表， thread 才代表

Runnable 子类对象， 并不代表线程，它只代表，要在线程中执行的任务

线程就是一条执行路径，至于在线程这条执行路径上，究竟执行的是什么样的具体代码，与线程没有关系的

### 继承 Thread 与 实现 Runnable 两种方式的比较?

**Thread**

Runnable 实现步骤少

实现方式，存在单重继承的局限性

**Runnable**

将线程与任务解藕

便于多线程数据的共享


### 什么时候会产生数据安全问题?

多线程运行环境

多线程访问共享数据

存在一个非原子操作

**有重复的票**
![](https://img.fengqigang.cn//img/20210421112502.png)

**有不存在的票**
![](https://img.fengqigang.cn//img/20210421113130.png)

### 什么是原子操作?

一个操作要么一次执行完，一次都不执行

![](https://img.fengqigang.cn//img/20210421112013.png)

**tickets**

不是原子操作

### 如何解决数据安全问题?

逻辑上， 解决把 **一组操作变成原子的操作** 的这件事情

**思路1:**

只在一个线程上，对共享变量的一组操作的执行过程，能够阻止线程切换

**无法实现** 

java 是采取抢占式线程调度，代码层面(线程中执行的代码), 无法控制线程调度

**思路2:**

把共享变量，加一把锁，利用锁来实现原子的操作，使用锁，可以给共享加锁，从面保证:

a. 只有加锁的线程，能够访问到共享变量

b. 在加锁线程中，没有完成对共享变量的一组操作之前，不会释放锁

c. 只要不释放锁，其他线程，即使被调度执行，也无法访问共享变量

### 什么是 **synchronized** 同步?

1. 同步的代码块中的锁对象可以是任意的 java 对象

2. 一定要保证是同一个对象


![](https://img.fengqigang.cn//img/20210421115103.png)



