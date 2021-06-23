---
title: "20_thread"
date: 2021-04-21T17:00:51+08:00
lastmod: 2021-04-21
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### What's `thread` and `multithreaded`?

Individual programs will appear to do multiple tasks at the same time.

Each task is executed in a `thread`, which is short for thread of control.

Programs that can run more than one thread at once are said to be `multithreaded`


### What's the difference between `multiple processes` and `multiple threads`?

`each process` has a complete set of its own variable

`thread` share the same data. Shared variables make communication between threads more efficient and easier to program than interprocess communication.

**on some operating systems, threads are more "lightweight" than process - it takes less overhead to create and destroy individual threads than it does to launch new processes.**


### 如何实现程序睡眠3秒?

**TimeUnit.SECONDS.sleep(3)；**

```java
public class TestSleep {
    static boolean flag = true;

    public static void main(String[] args) throws InterruptedException {
        sayHelloRecycling();
    }

    private static void sayHelloRecycling() throws InterruptedException {
        while(flag){
           System.out.println("你好");
           TimeUnit.SECONDS.sleep(3);
        }
    }
}
```

![](https://img.fengqigang.cn//img/20210420105542.png)

### 什么是进程?

操作系统进行 **资源分配与调度** 的基本单位.

一个正在运行的程序，软件都可以称为进程

**进程之间是互不干扰的**

### 什么是线程?

CPU 进行 **资源分配与调试** 的基本单位，从执行路径的角度来看在，**每一条执行路径都是1个线程**

### 进程和线程的关系？

线程依赖于进程而存在

**线程之间是共享进程资源的**

一个进程可以有 **最少一个线程**

### 什么是串行, 并行，并发?

**串行**:

一个任务接一个任务 **按顺序执行**

![](https://img.fengqigang.cn//img/20210420110810.png)

**并行**:

在一个 **时间点** 上，多个任务同时执行

![](https://img.fengqigang.cn//img/20210420110921.png)

**并发**:

在一个 **时间段** 上， 多个任务同时执行

![](https://img.fengqigang.cn//img/20210420111011.png)

### 什么是单道批处理?

**单道**:

在整个操作系统中，同一时间，内存中只有一个程序

只能是上一个程序运行完，下一个程序才能开始运行

**批处理**:

在程序运行过程中，不会有任何响应，直到程序运行结束

### 什么是多道批处理?

**多道**：

在操作系统中，同时内存中，可以有多个应用程序，在运行, 这样一来，一旦某个应用程序， 不需要使用cpu的计算功能.操作系统就会把cpu计算时间，分配给内存中的其他应用程序来计算，这样一来，cpu的资源利用率就大提高了

**多道批处理**:

当应用程序，占用cpu执行时间，，这个应用才算真正的执行, 在多道批处理系统中，多个应用程序，交替执行，看起来好像多个应用程序在"同时"运行.

### 为什么有了进程还要有线程?

**进程的上下文切换**:

1.  保护现场 （值， 寄存器的状态保存到一个地址）
2.  恢复现场 （恢复寄存器的值， 寄存器的状态）

![](https://img.fengqigang.cn//img/20210420112632.png)

为了提高切换的效率，引入了 **线程(轻量进程)**

**每一个线程负责一个子任务**

线程上下文线程中切换的代价要小

### **Java** 程序运行程序的原理是什么？

1.  运行 **Java** 命令会创建 **jvm** 进程
    
2.  **jvm** 进程会去创建一个 **main** 线程
    

3。 回到 **main** 线程中 执行 **main()** 方法

### 如何验证 **jvm** 是单线程还是多线程的?

![](https://img.fengqigang.cn//img/20210420113251.png)

有GC线程回收

所以 **jvm** 是多线程的, 至少还有一个垃圾回收线程

### How to procedure for running a task `in a separate thread` ?

1. Place the code for the task into the `run` method of a class that implements the `Runnable` interface

![20210518225757](https://img.fengqigang.cn//img/20210518225757.png)

**Since `Runnable` is a functional interface, could make an instance with lambda expression**

```java
Runnable r = () -> {task code};
```


2. Construct a `Thread` object from the `Runnable`:

```java
var t = new Thread(r);
```

3. Start the thread 

```java
t.start();
```

![20210518230308](https://img.fengqigang.cn//img/20210518230308.png)


### When I procedure for running a task `in a separate thread`, why not call the `run` to start thread ?

Calling the `run` method directly merely executes the task in the same thread -- no new thread is started.

### How to define a thread by forming a subclass of the `Thread` class?

```java
class MyThread extends Thread{
	public void run(){
		task code
	}
}
```

**This approach is no longer recommended.**

You should decouple the task that is to be run in parallel from the mechanism of running it. If you have many tasks, it is too expensive to create a separate thread for each of them.

Instead, you can use a thread pool.


### 为什么要重写 **Thread** 类中的 **run** 方法?

只有 **Thread run()** 方法中的代码， 都会执行在 **子线程** 中

### 同一个 **Thread** 或 **Thread** 子类可以被启动多次吗?

不可以， 同一个 **Thread** 或 **Thread** 子类 只能启动一次

可以创建多个线程对象，并启动这些线程对象

```java
public class Demo {
    public static void main(String[] args) {
        System.out.println("main start");

        // 创建子类对象
        MyThread myThread = new MyThread();
        myThread.start();
        myThread.start();
    }
}

class MyThread extends Thread {

    @Override
    public void run() {
        try {
            TimeUnit.SECONDS.sleep(3);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        for (int i = 0; i < 10; i++) {
            System.out.println(i);
        }
        call();
    }

    public static void call() {
        System.out.println("call");
    }
}
```

![20210420184227](https://img.fengqigang.cn//img/20210420184227.png)

### 要想让代码在子线程中运行，只能将代码在 **run** 方法体中吗?

一个方法 ，被哪个线程中的代码调用，被调用的方法，就运行在，调用它的线程中

```java
public class Demo {
    public static void main(String[] args) {
        System.out.println("main start");

        // 创建子类对象
        MyThread myThread = new MyThread();
        myThread.start();
    }
}

class MyThread extends Thread {

    @Override
    public void run() {
        try {
            TimeUnit.SECONDS.sleep(3);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        for (int i = 0; i < 10; i++) {
            System.out.println(i);
        }
        call();
    }

    public static void call() {
        System.out.println("call");
    }
}
```

![20210420184342](https://img.fengqigang.cn//img/20210420184342.png)

![](https://img.fengqigang.cn//img/20210420144507.png)

### 如何获取子线程名称?

getName

public final String getName()

Returns this thread's name

```java
public class Thread1 {
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            System.out.println(i);
        }

        MyThread myThread = new MyThread();
        myThread.start();
    }
}

class MyThread extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println(getName() + "------" + i);
        }
    }
}
```

### 如何获取主线程名称?

**currentThread**

public static Thread currentThread()

Returens a reference to the currently executing thread object.

```java
public class Thread1 {
    public static void main(String[] args) {
        MyThread myThread = new MyThread();
        myThread.setName("王冰冰");

        myThread.start();
        Thread thread = Thread.currentThread();
        String name = thread.getName();
        for (int i = 0; i < 10; i++) {
            System.out.println(name + "---------" + i);
        }
    }
}

class MyThread extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println(getName() + "------" + i);
        }
    }
}
```

### 如何设置线程名称?

setName

public final void setName(String name)

Changes the name of this thread to be equal to the argument name.

```java
public class Thread1 {
    public static void main(String[] args) {
        MyThread myThread = new MyThread();
        myThread.setName("王冰冰");

        myThread.start();
        Thread thread = Thread.currentThread();
        String name = thread.getName();
        for (int i = 0; i < 10; i++) {
            System.out.println(name + "---------" + i);
        }
    }
}

class MyThread extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println(getName() + "------" + i);
        }
    }
}
```

### 如何设置主线程名称?

方法一(通过 **CurrentThread**):

```java
public class Thread1 {
    public static void main(String[] args) {
        MyThread myThread = new MyThread();
        myThread.setName("王冰冰");

        myThread.start();
        Thread thread = Thread.currentThread();
        thread.setName("长风");
        String name = thread.getName();
        for (int i = 0; i < 10; i++) {
            System.out.println(name + "---------" + i);
        }
    }
}

class MyThread extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println(getName() + "------" + i);
        }
    }
}
```

方法二(**用构造方法**):

Thread(String name)

Allocates a new Thread object

```java
public class Thread1 {
    public static void main(String[] args) {
        MyThread myThread = new MyThread("王冰冰");

        myThread.start();
        Thread thread = Thread.currentThread();
        thread.setName("长风");
        String name = thread.getName();
        for (int i = 0; i < 10; i++) {
            System.out.println(name + "---------" + i);
        }
    }
}

class MyThread extends Thread {


    public MyThread(String name) {
        super(name);
    }

    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println(getName() + "------" + i);
        }
    }
}
```

### 线程调度的方式?

协同式线程调度

抢占式线程调度

### 什么是线程调度?

线程调度是指系统为线程 **分配处理器使用权** 的过程

### 什么是协同式线程调度? 它有什么好处?

线程的执行时间， 由线程本身来控制

线程把自己的工作执行完后，主动通知系统切换到另外一个线程上去

**好处**

实现简单

**环处**

执行时间不可控

### 什么是抢占式线程调度?

每个线程将由系统来分配执行时间，线程的切换不由线程本身来决定

**好处**

执行时间是可控的

### java 用的是什么线程调度?

抢占式线程调度


### What is the priority of a Thread in Java?

- You can increase or decrease the priority of the thread with the `setPriority` method.

```java
myThread.setPriority(Number);
```

- You can set the priority to any value between `MIN_PRIORITY` and `MAX_PRIORITY`
		- MIN_PRIORITY `defined as 1`
		- NORM_PRIORITY `defined as 5`
		- MAX_PRIORITY `defined as 10`

![20210519085633](https://img.fengqigang.cn//img/20210519085633.png)

- Whenever the thread scheduler has a chance to pick a new thread, it prefers threads with higher priority.

- However, thread priorities are `highly system-dependent`

- When the virtual machine relies on the thread implementation of the host platform, the Java thread priorities are mapped to the priority level of the host platform, which may have more or fewer thread priority levels.

- For example, Windows have seven priority levels. Some of the Java priorities will map to the same operating system level. In the `Oracle JVM for Linux`, thread priorities are ignored altogether -- all threads have the priority levels.

**Thread priorities may have been useful in early versions of Java that don't use operating Systems threads. You should not use them nowadays.**


### 如何获取优先级？

getPriority

public int getPriority()

Ruturns the thead priority of the thread associated with this ThreadInfo

```java
public class Demo {
    public static void main(String[] args) {
        System.out.println("main start");
        // 创建子类对象
        MyThread myThread = new MyThread();
        int priority = myThread.getPriority();
        myThread.setName("main线程");
        System.out.println(myThread.getName() + "默认的priority是:" + myThread.getPriority);

        myThread.start();
    }
}

class MyThread extends Thread {

    @Override
    public void run() {
        try {
            TimeUnit.SECONDS.sleep(3);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        for (int i = 0; i < 10; i++) {
            System.out.println(i);
        }
        call();
    }

    public static void call() {
        System.out.println("call");
    }
}
```

![20210420185807](https://img.fengqigang.cn//img/20210420185807.png)

### 为什么设置两个不同的优先级看起来没有用?

1.  操作系统的优先级是 **动 \+ 静**
    
2.  **java** 当中提高的是静态优先级
    
3.  它只是一个对操作系统的建议，操作系统不一定采纳
    

**java官方**:

线程优先级并非完全没有用，**Thread** 的优先级，它具有统计意义，总的来说，高优先级的线程占用的cpu执行时间多一点，低优先级线程，占用cpu执行时间，短一些

### 如何休眠一个线程?

static void sleep(long millis)

Causes the currently executing thread to sleep (temporarily cease execution) for the specified number of milliseconds, subject to the precision and accuracy of system timers and schedulers.

```java
public class Demo {
    public static void main(String[] args) {
        ThreadSleep threadSleep = new ThreadSleep();
        threadSleep.setName("UZi");
        threadSleep.start();
    }
}

class ThreadSleep extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println(getName() + "-----" + i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

![20210420191007](https://img.fengqigang.cn//img/20210420191007.png)

### 如何合并线程?

public final void join()
Waits for this thread to die.
An invocation of this method behaves in exactly the same way as the invocation

**未使用 join()**

```java
public class Demo {
    public static void main(String[] args) {
        System.out.println("main start");

        ThreadJoin threadJoin = new ThreadJoin();
        threadJoin.setName("子线程");
        threadJoin.start();
        System.out.println("main end");

    }
}

class ThreadJoin extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println(getName() + "-----" + i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

![20210420191900](https://img.fengqigang.cn//img/20210420191900.png)

**加入 join()**

```java
public class Demo {
    public static void main(String[] args) throws InterruptedException {
        System.out.println("main start");

        ThreadJoin threadJoin = new ThreadJoin();
        threadJoin.setName("子线程");
        threadJoin.start();
        threadJoin.join();
        System.out.println("main end");

    }
}

class ThreadJoin extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println(getName() + "-----" + i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

![20210420192019](https://img.fengqigang.cn//img/20210420192019.png)

**start 要在 join 前**

![](https://img.fengqigang.cn//img/20210420160536.png)

![](https://img.fengqigang.cn//img/20210420160751.png)

### 线程中若使用 join 谁等待? 等待谁?

**谁等待**

哪个线程调用了 **join** 代码，哪个线程就等待

**等待谁**

等待子线程， 等待的是调用了 **join** 这个线程

### 线程是如何分类的？

守护线程

用户线程

**线程默认是用户线程**

### GC是什么线程?

守护线程

### How to turn a thread into a daemon thread?

```java
t.setDaemon(true);
```

When only daemon threads remain, the virtual machine exits.

This method must be invoked before the thread is started.

在 **start** 后执行会报错

![20210420193411](https://img.fengqigang.cn//img/20210420193411.png)

**设置成守护线程后, main死亡时, 线程也会死亡**

1.  未使用时

![20210420193611](https://img.fengqigang.cn//img/20210420193611.png)

2.  使用时

![20210420193637](https://img.fengqigang.cn//img/20210420193637.png)

### 什么是礼让线程?

yield

public static void yield()

A hint to the scheduler that the current thread is willing to yield its current use of a processor. The scheduler is free to ignore this hin

```java
public class Demo {
    public static void main(String[] args) throws InterruptedException {
        ThreadYield t1 = new ThreadYield();
        ThreadYield t2 = new ThreadYield();
        t1.setName("吴彦祖");
        t2.setName("彭于晏");
        t1.start();
        t2.start();
    }
}

class ThreadYield extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println(getName() + "------" + i);
            Thread.yield();
        }
    }
}
```

![20210420194127](https://img.fengqigang.cn//img/20210420194127.png)

### 为什么使用yield后，没有起到抢占式的结果?![20210420194127](https://img.fengqigang.cn//img/20210420194127.png)

吴彦祖虽然放弃了CPU的执行权

但 **Java** 中采用的是抢占式的调试方式

吴彦祖又抢到了

### 如何中断线程对象(interrupt 会发生什么)?

**interrupt**

public boolean isInterrupted()

Tests whether this thread has been interrupted. The interrupted status of the thread is unaffected by this method.

A thread interruption ignored because a thread was not alive at the time of the interrupt will be reflected by this method returning false.

Returns:
true if this thread has been interrupted; false otherwise.

```java
public class Demo {
    public static void main(String[] args) throws InterruptedException {
        ThreadInterrupt thread = new ThreadInterrupt();
        thread.setName("送终鸡");

        thread.start();
        try {
            Thread.sleep(3000);
        } catch (InterruptedException e){
           e.printStackTrace();
        }
        thread.interrupt();
    }
}

class ThreadInterrupt extends Thread{
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println(getName() + "-----" + i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
              e.printStackTrace();
            }
        }
    }
}
```

![20210420194937](https://img.fengqigang.cn//img/20210420194937.png)

### 如何中断线程对象(stop 会发生什么)?

stop
@Deprecated
public final void stop()

Deprecated. This method is inherently unsafe.

会终止线程执行

```java
public class Demo {
    public static void main(String[] args){
        ThreadStop threadStop = new ThreadStop();
        threadStop.setName("短风");
        threadStop.start();
        try{
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        threadStop.stop();
    }
}

class ThreadStop extends Thread{
    @Override
    public void run() {
        System.out.println("ThreadStop start");
        for (int i = 0; i < 10; i++) {
            System.out.println(getName() + "-----" + i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println("ThreadStop end");
    }
}
```

![20210420195440](https://img.fengqigang.cn//img/20210420195440.png)

### 如何安全终止线程？(用 **flag** 标记， 如果为 true, 正常执行， 如果为 false, 终止线程执行, 在终止之前，去做一个日志保存，将终止信息保存到 og.txt 当中, 利用 FileWriter, 2021-4-28 时分秒 : 某个线程终止了)

```java
import java.io.FileWriter;
import java.io.IOException;
import java.text.SimpleDateFormat;
import java.util.Date;

/**
 * @className: Demo
 * @Description
 * @author: fengxiaonan
 * @date: 4/20/21 6:38 PM
 */
public class Demo {
    public static void main(String[] args) throws InterruptedException {
        ThreadStop thread = new ThreadStop();
        thread.setName("子线程");
        thread.start();

        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        thread.flag = false;
    }
}

class ThreadStop extends Thread {
    boolean flag = true;

    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            if (flag) {
                System.out.println(getName() + "-----" + i);
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            } else {
                try {
                    FileWriter fileWriter = new FileWriter("log.txt");
                    SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm::ss");
                    String date = simpleDateFormat.format(new Date());
                    fileWriter.write(date + " " + getName() + "被终止了!");
                    fileWriter.write(System.lineSeparator());
                    fileWriter.flush();
                    fileWriter.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

![20210420200244](https://img.fengqigang.cn//img/20210420200244.png)


### How many states of thread in Java?

Threads can be in one of six states:

- new 
- Runnable
	- A runnable therad may or may not be running at any given time.(This is why the state is called "runnable" and not "running")
- Blocked
- Waiting
- Timed waiting
- Terminated


![20210518233244](https://img.fengqigang.cn//img/20210518233244.png)

### what is Preemptive scheduling systems and cooperative scheduling?

- Preemptive scheduling systems

Preemptive scheduling systems give each runnable thread a slice of time to perform its task.

When that slice of time is exhausted, the operating system preempts the thread and gives another thread an opportunity to work.

When selecting the next thread, the operating system takes into account the thread priorities.

**All modern desktop and server operating systems use preemptive scheduling.**

- Cooperative scheduling systems

A thead loses control only when it calls the `yield` mehtod, or when it is blocked or waiting.

**small devices such as cell phones may use cooperative scheduling.**



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

1.  实现 Runnable 接口
    
2.  重写 run 方法
    
3.  创建 Runnable 子类对象
    
4.  创建 Thread 对象， 并且把 Runnable 子类对象作为参数传递
    
5.  start 方法
    

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


### 什么是原子操作?

一个操作要么一次执行完，一次都不执行

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

1.  同步的代码块中的锁对象可以是任意的 java 对象
    
2.  一定要保证是同一个对象
    

![](https://img.fengqigang.cn//img/20210421115103.png)


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

### 用 **Callable** 方式，启动2个线程， 1个从1一直加到100， 一个从1一直加到200，最后打印结果

![](https://img.fengqigang.cn//img/20210423100625.png)

### Timer 如何使用(schedule(TimerTask task, Data time))?

![](https://img.fengqigang.cn//img/20210423101903.png)

### Timer 如何使用(schedule(TimerTask task, long delay, long period))?

![](https://img.fengqigang.cn//img/20210423102101.png)

### Timer 如何使用(schedule(TimerTask task, Date firstTime, long period))?

![](https://img.fengqigang.cn//img/20210423102214.png)





