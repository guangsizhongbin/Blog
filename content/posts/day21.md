---
title: "Day21"
date: 2021-04-23T09:17:16+08:00
lastmod: 2021-04-23
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### 同步方法中的锁对象是什么?

**同步代码块中**

任意java对象

**任意方法中**

this

**静态方法中**

字节码文件对象（.clsss）
![](https://img.fengqigang.cn//img/20210422095504.png)

**补充代码**

![](https://img.fengqigang.cn//img/20210422095648.png)

### 为什么在同步代码块中可以放一个任意的对象?

1.  因为 **java** 当中所有对象， 内部都存在一个 **标志位**，表示加锁和解锁的状态
2.  其实锁对象，就是充当锁的角色

所谓的加锁解锁，其实就是 **设置锁对象的标志位**，来表示加锁解锁的**状态**

### 当某个线程执行到同步代码块时，遇到加锁或无锁时会怎么处理?

1.  当锁对象处于**未加锁**状态， **jvm** 就会设置锁对象的标志位(加锁)， 并在锁对象中记录，是哪个线程加的锁. 加锁成功， 执行同步代码块中的代码。
2.  如果锁对象 **已经被加锁**, 且加锁线程不是当前线程，系统会让当前线程处于阻塞状态(等着)， 直到加锁线程，执行完了对共享变量的组操作，并释放锁。

### 加锁线程何时释放锁?

当加锁线程，执行完了同步代码块中的代码(对共享变量的一组操作)，**在退出同步代码块之前**,

**jvm** 自动清理锁对象的标志位，将锁对象变成未上锁状态(释放锁)

### 如何使用 Lock 锁住对象?

1.  定义一把锁

Lock lock = new ReentrantLock();

美\[ˌriˈɛntrənt\]

public ReentrantLock()

Creates an instance of ReentrantLock. THis is equivalent to using ReentrantLock(false).

2.  获取锁

lock.lock();

void lock()

Acquires the lock.

3.  释放锁

lock.unlock;

void unlock()

Releases the lock.

![](https://img.fengqigang.cn//img/20210422101202.png)

### Lock 和 synchronized 的区别?

synchronized 会同步阻塞

**synchronized**

只提供了用来 **模拟锁状态的标志位** (加锁和释放锁)

加锁和释放锁的行为，都是由 **jvm** 隐式完成(**和 synchronized 锁对象没有关系**)

所以 synchronized 锁对象 **不是一把完整的锁**

**Lock**

它代表的是完整的锁

Lock对象， 它如果要实现加锁和释放锁，不需要 synchronized 关键字配合，**它自己就可以完成**

Lock(接口):

lock() 加锁 unlock 释放锁

### 什么是同步与异步?

同步与异步描述的是被调用者的

如 A 调用 B:

如果是 **同步** ，B 在接到 A 调用后，会立即执行要做的事。 A 的本次调用可以得到结果.

如果是 **异步** ，B 在接到 A 调用后，不保证会立即执行要做的事，但是保证会去做， B 在做好了之后会通知 A。 A的本次调用得不到结果， 但是 B 执行完之后会通知 A .

![](https://img.fengqigang.cn//img/20210422102202.png)

![](https://img.fengqigang.cn//img/20210422110800.png)

### 什么是死锁?

2 个或以上的线程争抢资源，造成互相等待的现象

![](https://img.fengqigang.cn//img/20210422111209.png)

### 在 **java** 中怎样的代码容易产生死锁?

一般出现在 **同步代码块嵌套**

![](https://img.fengqigang.cn//img/20210422111342.png)

![](https://img.fengqigang.cn//img/20210422112110.png)

### 解决死锁的方法有哪些?

**方式一** 更改加锁顺序

![](https://img.fengqigang.cn//img/20210422112613.png)

**方式二**: 将该步骤变成原子操作

最外层再加一层操作

![](https://img.fengqigang.cn//img/20210422113238.png)

### 什么是生产者消费者模型?

![](https://img.fengqigang.cn//img/20210422113915.png)

![](https://img.fengqigang.cn//img/20210422144721.png)

### 线程间通信有哪些API?

1.  wait() 阻止自己
    
2.  notify() 通知别人
    
3.  notifyAll() 通知所有的人
    

### 线程间通信的 wait() api 是干什么的?

public final void wait

throws InterruptedException

1.  阻塞功能:

当在某线程中，对象上 **.wait()**, 在哪个线程中调用 **wait()**, 导致哪个线程处于阻塞状态

当某线程，因为调用执行某对象的 **wait()**, 而处于阻塞状态，我们说，该线程在该对象上阻塞

2.  唤醒条件

当某线程，因为某对象A的 **wait()**, 而处于阻塞状态时，如果要唤醒该线程，只能在其他线程中，再同一个对象 (即对象A) 上调用其 **notify()** 或 **notifyAll()**

即在线程的阻塞对象上，调用 **notify** 或 **notifyAll** 方法，才能唤醒，在该对象上阻塞的线程

3.  运行条件

当前线程必须拥有此对象 **监视器**

监视器: 指 **synchronized** 代码块中的锁对象

如果不在同步代码块中调用就会就会出现 **IllegalMonitorStateException**

4.  执行特征

该线程释放对监视器的所有权

等待(阻塞)

### Thread 的 **sleep** 方法， 执行时会丢失监视器的所属权吗?

不会

### Object 的 **wait** 方法， 执行时会丢失监视器的所属权吗?

会

### Thread.sleep VS Object.wait()?

1.  所属不同:
    
    **sleep**
    
    定义在**Thread**类，静态方法
    
    **wait**
    
    定义在**Object**类中，非静态方法
    
2.  唤醒条件不同
    
    **sleep**
    
    休眠时间到
    
    **wait**
    
    在其他线程中，在同一个锁对象上，调用了 **notify** 或 **notifyAll** 方法
    
3.  使用条件不同
    
    **sleep**
    
    没有任何前提条件
    
    **wait**
    
    必须是当前线程，持有锁对象，锁对象上调用 **wait()**
    
4.  休眠时，对锁对象的持有，不同:
    
    **sleep**
    
    处于阻塞状态的时候，在阻塞的时候不会放弃对锁的持有
    
    **wait**
    
    处于阻塞的时候，会放弃对象持有3
    

### notify() api 是干什么的?

public final void notify()

唤醒在此对象监视器上等待的单个线程

如果所有线程都在此对象上等待

则 **会选择唤醒其中一个线程， 选择是任意性的**

### 产包子实战？

1.  **生产者**

![](https://img.fengqigang.cn//img/20210422150944.png)

2.  **消费者**

![](https://img.fengqigang.cn//img/20210422151228.png)

3.  **蒸笼**

![](https://img.fengqigang.cn//img/20210422151830.png)

3.  **demo**
    ![](https://img.fengqigang.cn//img/20210422151638.png)

### 如何产生随机数?

```java
Random random = new Random();
// nextInt(int bound)  [0, bound]
int i = random.nextInt(foods.length);
```

### 只执行一次?

![](https://img.fengqigang.cn//img/20210422150505.png)

### 同步方法

1.  Box

![image-20210422161723697](C:%5CUsers%5Cfeng%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20210422161723697.png)

2.  Box
    ![](https://img.fengqigang.cn//img/20210422161748.png)

### 为什么多个生产者，消费者的时候，会出现卡顿？

![](https://img.fengqigang.cn//img/20210422163134.png)

### 什么是 **虚假唤醒**?

唤醒了不应该被唤醒的线程

### 为什么 **wait**,**notify**, 为啥不定义在 Thread 当中?

因为锁对象可以是任意java对象

### 完整的线程转换图是什么?

![](https://img.fengqigang.cn//img/20210422164308.png)

### 为什么会有线程池?

![](https://img.fengqigang.cn//img/20210422171154.png)

### 三种线程池?

![](https://img.fengqigang.cn//img/20210422171305.png)

**带缓存的线程池**

![](https://img.fengqigang.cn//img/20210422171734.png)

**newFixedThreadPod**

![](https://img.fengqigang.cn//img/20210422172146.png)

### 如何实现 newFixedThreadPod?

![](https://img.fengqigang.cn//img/20210422173017.png)

### ![](https://img.fengqigang.cn//img/20210422173033.png)? 有什么区别?

shutdownNow 队列中也执行

shutdownNow 队列中的不执行

### 如何实现 **Callable**?

![](https://img.fengqigang.cn//img/20210422173906.png)

### **Future** 是干什么的?

![](https://img.fengqigang.cn//img/20210422173946.png)

### Runnable VS Callable

![](https://img.fengqigang.cn//img/20210422174325.png)

### FutureTask 如何使用?

![](https://img.fengqigang.cn//img/20210422174806.png)

![](https://img.fengqigang.cn//img/20210422174931.png)


