---
title: "Day19"
date: 2021-04-20T20:03:24+08:00
lastmod: 2021-04-20
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

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

1. 保护现场 （值， 寄存器的状态保存到一个地址）
2. 回复现场 （恢复寄存器的值， 寄存器的状态）

![](https://img.fengqigang.cn//img/20210420112632.png)

为了提高切换的效率，引入了 **线程(轻量进程)**

**每一个线程负责一个子任务**

线程上下文线程中切换的代价要小

### **Java** 程序运行程序的原理是什么？

1. 运行 **Java** 命令会创建 **jvm** 进程

2. **jvm** 进程会去创建一个 **main** 线程

3。 回到 **main** 线程中 执行 **main()** 方法

### 如何验证 **jvm** 是单线程还是多线程的?

![](https://img.fengqigang.cn//img/20210420113251.png)

有GC线程回收

所以 **jvm** 是多线程的, 至少还有一个垃圾回收线程

### 用继承 Thread 类实现多线程?

1. 继承 **Thread**类

2. 重写 **run** 方法

3. 创建子类对象

4. 通过 **start** 方法启动一个线程


为什么不用 **run** 方法?

用 **run** 不是启动多线程，只是当作普通方法调用



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

###  要想让代码在子线程中运行，只能将代码在 **run** 方法体中吗?

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

public final voied setName(String name)

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

### 线程优先级?

![](https://img.fengqigang.cn//img/20210420151740.png)

MAX_PRIORITY 为 10

MIN_PRIORITY 为 1

NORM_PRIORITY 为 5

### 如何设置优先级？

public final void setPriority(int newPriority)

changes the priority of the thread.

```java
public class Demo {
    public static void main(String[] args) {
        System.out.println("main start");
        // 创建子类对象
        MyThread myThread = new MyThread();
        int priority = myThread.getPriority();
        myThread.setName("main线程");
        System.out.println(myThread.getName() + "默认的priority是:" + myThread.getPriority());
        myThread.setPriority(myThread.MAX_PRIORITY);
        System.out.println(myThread.getName() + "改变后的priority是:" + myThread.getPriority());


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

![20210420190158](https://img.fengqigang.cn//img/20210420190158.png)


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

1. 操作系统的优先级是 **动 + 静**

2. **java** 当中提高的是静态优先级

3. 它只是一个对操作系统的建议，操作系统不一定采纳

**java官方**:

线程优先级并非完全没有用，**Thread** 的优先级，它具有统计意义，总的来说，高优先级的线程占用的cpu执行时间多一点，低优先级线程，占用cpu执行时间，短一些


### 如何休眠一个线程?

static void	sleep(long millis)

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

## GC是什么线程?

守护线程

### 如何将线程标记为守护线程?

public final void setDaemon(boolean on)

![](https://img.fengqigang.cn//img/20210420161854.png)

Marks this thread as either a daemon thread or a user thread. 

The Java Virtual Machine exits when the only threads running are all daemon threads.

This method must be invoked before the thread is started.

在 **start** 后执行会报错

![20210420193411](https://img.fengqigang.cn//img/20210420193411.png)

**设置成守护线程后, main死亡时, 线程也会死亡**

1. 未使用时

![20210420193611](https://img.fengqigang.cn//img/20210420193611.png)

2. 使用时

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



