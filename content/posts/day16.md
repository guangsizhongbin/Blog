---
title: "Day16"
date: 2021-04-16T21:49:13+08:00
lastmod: 2021-04-16
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### 字节流是怎么分类的?

- 字节输出流
		- 抽象基类
			- OutputStream
		- 具体子类
			- FileOutputStream
			- BufferedOutputStream

- 字节输入流
		- 抽象基类
			- InputStream
		- 具体子类
			- FielInputStream
			- BufferedInputStream

### 字符流是怎么分类的？

- 字符输出流

- 字符输入流

### 什么是IO?

i: input 输入

o: output 输出

### 为什么会有 IO?

需要长久保存的数据都是以文件的形式存储的，存储在外边设备当中

内存有限，需要把数据读取到内存才行，需要io交互


### **java** 流模型是什么样的?

![](https://img.fengqigang.cn//img/20210416153623.png)


### **java** 中的流是怎么分类的?

- 按照流向分(以内存为参照)
	- 输入流 input
	- 输出流 output
- 按照数据类型分类
	- 字节流: 一连串的 01 二进制数据 按字节传输 1B = 8 bit 0000 0000
	- 字符流: 一连串的字符的字符序列，把它当做一种文化符号 "abc", "你"


![](resources/9473bff75028444a99ed508d4e9fe50e.png)

### **java** IO抽象基类有哪些?

- 字节输出流 OutputStream
- 字节输入流 InputStream
- 字节输出流 Writer
- 字符输入流 Reader

**由这4个基类派生出的子类,其子类名都是以父类名作为后缀**


### **OutpuStream** 的继承关系?

![](https://img.fengqigang.cn//img/20210416154738.png)


### **outputStream** 的 **write** 的实现原理是什么样的?

**public abstract void write(int b) throws IOException**

将指定的字节写入此输出流， **write** 的常规协定是: **向输出流写入一个字节，要写入的字节是参数b的八个低位，b的24个高位将被忽略**


### **FileOutputStream(File file)**, 如何实现?

![](https://img.fengqigang.cn//img/20210416155431.png)


![](https://img.fengqigang.cn//img/20210416155526.png)


### 为什么用 IO 一定要关闭资源?

它属于操作系统，与 **java** 无关，只能显式的释放资源(如 wps资源) 软件占用.


### 如何用 **FileOutputStream** 用 **write** 方法?

```java
public class Demo {
    public static void main(String[] args) throws IOException {
        FileOutputStream out = new FileOutputStream( new File("b.txt"));
        out.write(97);
        out.close();
    }
}
```

### 如何用 **FileOutputStream** 用 **write(byte[] b)**

**byte[] getBytes(String charsetName)**

Encodes this String into a sequence of bytes using the name charset, storing the result into a new byte array.


```java
public class Demo {
    public static void main(String[] args) throws IOException {
        FileOutputStream out = new FileOutputStream( new File("b.txt"));
        String s = "abc";
        byte[] bytes = s.getBytes();
        out.write(bytes);
    }
}
```

### 如何用 **write(byte[] b , int off, int len)**?


```java
public class Demo {
    public static void main(String[] args) throws IOException {
        FileOutputStream out = new FileOutputStream( new File("b.txt"));
        String s = "abc";
        byte[] bytes = s.getBytes();
        out.write(bytes, 0, bytes.length);
    }
}
```

### 创建字节输出流对象发生了什么事情?

1. 创建之前 **jvm** 会去操作系统中找该文件是否存在
2. 如果不存在，帮我们创建
3. 如果存在，会清空重写
4. 创建之后就建立起内存与外设的数据通道

### **FileOutputStream** 如何实现数据追加?

**public FileOutputStream(File file, boolean append) throw FIleNotFoundException**

```java
public class Demo {
    public static void main(String[] args) throws IOException {
        FileOutputStream out = new FileOutputStream( "b.txt", true);
        out.write("def".getBytes());
        out.close();
    }
}
```

### **FileOutputStream** 如何实现换行?

**\n**

```java
public class Demo {
    public static void main(String[] args) throws IOException {
        FileOutputStream outputStream = new FileOutputStream("a.txt", true);
        outputStream.write("\n".getBytes());
        outputStream.write("def".getBytes());
        outputStream.close();
    }
}
```

**System.lineSeparator()**

```java
public class Demo {
    public static void main(String[] args) throws IOException {
        FileOutputStream outputStream = new FileOutputStream("a.txt", true);
        outputStream.write(System.lineSeparator().getBytes());
        outputStream.write("def".getBytes());
        outputStream.close();
    }
}
```

**\r**

```java
public class Demo {
    public static void main(String[] args) throws IOException {
        FileOutputStream outputStream = new FileOutputStream("a.txt", true);
        outputStream.write("\r".getBytes());
        outputStream.write("def".getBytes());
        outputStream.close();
    }
}
```

### **try-catch-with-resource** 的语法是什么? 如何实现?

**try...catch...source 会执行close**

```java
try(资源, 实现了Autocloseable接口){
// 代码
} catch() {

} finally {

}
```

```java
public class Demo {
    public static void main(String[] args) throws IOException {
        try (A a = new A()) {
            a.test();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

class A implements AutoCloseable {
    @Override
    public void close() throws Exception {
        System.out.println("close 方法执行了!!");
    }

    public void test() {
        System.out.println("test 执行了");
    }
}
```

![20210416195301](https://img.fengqigang.cn//img/20210416195301.png)

### **InputStream** 基类是什么样的?

![20210416195852](https://img.fengqigang.cn//img/20210416195852.png)

### **FileInputStrem** 构造方法是什么的?

**FileInputStream (File file)**

Creates a FileInputStream by opening a connection to an actual file, the file named by the File object in the file system.

**FIleInputStream (String name)**

Creates a FileInputStream by opening a connection to an actual file, the file named by the path name in the file system.

```java
public class Demo {
    public static void main(String[] args) throws IOException {
        FileInputStream f1 = new FileInputStream(new File("a.txt"));
        FileInputStream f2 = new FileInputStream("a.txt");
    }
}
```

### **FileInputStream** 的 read 方法使用?

```java
public class Demo {
    public static void main(String[] args) throws IOException {
        FileInputStream in = new FileInputStream("a.txt");

        int readData = in.read();
        System.out.println(((char) readData));
        in.close();
    }
}
```

### ![20210416201037](https://img.fengqigang.cn//img/20210416201037.png) a 中是 abcdef 会输出什么?

abcd

efcd

![20210416201117](https://img.fengqigang.cn//img/20210416201117.png)

### 实现文件复制有什么思路?

**单字节复制 int 类型**

![20210416201352](https://img.fengqigang.cn//img/20210416201352.png)

**多字节 byte[] b**

![20210416201444](https://img.fengqigang.cn//img/20210416201444.png)

### 如何实现实现循环读取文件(单char)?

```java
public class Demo {
    public static void main(String[] args) throws IOException {
        FileInputStream in = new FileInputStream("a.txt");
        int readDate;
        while ((readDate = in.read()) != -1){
            System.out.println(((char) readDate));
        }
    }
}
```

![20210416202040](https://img.fengqigang.cn//img/20210416202040.png)

### 如何实现实现循环读取文件(用字节数组)?

```java
public class Demo {
    public static void main(String[] args) throws IOException {
        FileInputStream in = new FileInputStream("a.txt");
        int readDate;
        byte[] bytes = new byte[1024];
        while ((readDate = in.read(bytes)) != -1) {
            System.out.println(new String(bytes, 0, readDate));
        }
    }
}
```

[20210416202248](https://img.fengqigang.cn//img/20210416202248.png)

### 如何实现单字节复制文本文件(a.txt -> b.txt)

```java
public class Demo {
    public static void main(String[] args) throws IOException {
        FileInputStream in = new FileInputStream("a.txt");
        FileOutputStream out = new FileOutputStream("b.txt");
        int readData;
        while((readData = in.read())!=-1){
            out.write(readData);
        }
        out.close();
        in.close();
    }
}
```
### 如何实现统计复制文件的耗时(单字节的方式)?

**long start = System.currentTimeMillis();**

**long end = System.currenTimeMillis();**

```java
public class Demo {
    public static void main(String[] args) throws IOException {
        // 创建字节输入流对象
        FileInputStream in = new FileInputStream("a.txt");
        // 创建字节输出流对象
        FileOutputStream out = new FileOutputStream("c.txt");

        long start = System.currentTimeMillis();

        int readData;
        while ((readData = in.read()) != -1) {
            out.write(readData);
        }

        long end = System.currentTimeMillis();
        System.out.println("耗时:" + (end - start) + "ms");

        // close
        out.close();
        in.close();
    }
}
```


### 如何实现统计复制文件的耗时(字节数组String)?

**long start = System.currentTimeMillis()**

**long end = System.currentTimeMillis()**



```java
public class Demo {
    public static void main(String[] args) throws IOException {
        // 创建字节输入流对象
        FileInputStream in = new FileInputStream("a.txt");
        // 创建字节输出流对象
        FileOutputStream out = new FileOutputStream("c.txt");

        long start = System.currentTimeMillis();
        int readCount;
        byte[] bytes = new byte[1024];

        while ((readCount = in.read(bytes)) != -1) {
            out.write(bytes, 0, readCount);
        }

        long end = System.currentTimeMillis();
        System.out.println("耗时:" + (end - start) + "ms");

        // close
        out.close();
        in.close();
    }
}
```

### 如何复制的时候，什么时候选择字节流，什么时候选择字符流?

- 不知道用啥的时候就用字节流， 字节流是万能的

- 对于文本文件， 我们选择用字符流

### 什么是装饰器模式?

![20210416203647](https://img.fengqigang.cn//img/20210416203647.png)


```java
public class Demo {
    public static void main(String[] args) throws IOException {
        MilkTea milkTea = new MilkTea();
        milkTea.add();
        System.out.println("-------");
        DecoratorA decoratorA = new DecoratorA();
        decoratorA.setBeverage(milkTea);
        decoratorA.add();
        System.out.println("-------");
        DecoratorB decoratorB = new DecoratorB();
        decoratorB.setBeverage(decoratorA);
        decoratorB.add();
        System.out.println("-------");
        DecoratorC decoratorC = new DecoratorC();
        decoratorC.setBeverage(decoratorB);
        decoratorC.add();
        System.out.println("-------");

    }
}

// 饮料 蕨基类
abstract class Beverage {
    abstract void add();
}

// 奶茶类
class MilkTea extends Beverage {
    @Override
    void add() {
        System.out.println("老板，来杯奶茶, 加冰");
    }
}

// 装饰器类
class Decorator extends Beverage {
    public Beverage beverage;

    public void setBeverage(Beverage beverage) {
        this.beverage = beverage;
    }

    @Override
    void add() {
        beverage.add();
    }
}

class DecoratorA extends Decorator {
    @Override
    void add() {
        super.add();
        addZz();
    }

    private void addZz() {
        System.out.println("再加点珍珠");

    }
}

class DecoratorB extends Decorator {
    @Override
    void add() {
        super.add();
        addYg();
    }

    private void addYg() {
        System.out.println("再加点野果");
    }
}

class DecoratorC extends Decorator {
    @Override
    void add() {
        super.add();
        addHd();
    }

    private void addHd() {
        System.out.println("再加点红豆");
    }
}
```

![20210416214851](https://img.fengqigang.cn//img/20210416214851.png)

### 如何创建一个 **bufferOutStream** ?

|Constructor| Description|
|---|---|
|BufferedOutputStream \\ (OutputStream out)| Creates a new buffered output stream to write data to the specified underlying output stream|
|BufferedOutputStream \\ (OutputStream out, int size)| Creates a new buffered output stream to write data to the specified underlying output stream with the specified buffer size.|

```java
public class Demo {
    public static void main(String[] args) throws IOException {
        FileOutputStream out = new FileOutputStream("a.txt");
        BufferedOutputStream bo = new BufferedOutputStream(out);

        new BufferedOutputStream(new FileOutputStream( new File("a.txt")));

    }
}
```

![20210416203918](https://img.fengqigang.cn//img/20210416203918.png)

### 当流中有包装流，应该如何关闭流?

我们只需要关闭最外层的流即可

**close** 方法会执行 **flush** 方法

![20210416204558](https://img.fengqigang.cn//img/20210416204558.png)

### 如何创建一个 **bufferInputStream** ?

|Constructors| Description|
|----|----|
|BufferedInputStream \\ (InputStream in)| Creates a BufferedInputStream and save its arguemnt, the input stream in, for later use.|
|BufferedInputStream \\ (InputStream in, int size)| Creates a BufferInputStream with the specified buffer siez, and saves its arguemt, the input stream in, for later use.|

```java
public class Demo {
    public static void main(String[] args) throws IOException {
        BufferedInputStream br = new BufferedInputStream(new FileInputStream("a.txt"));

        //读数据
        int readData = br.read();
        System.out.println(((char) readData));
        br.close();
    }
}
```




