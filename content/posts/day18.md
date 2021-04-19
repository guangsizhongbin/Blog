---
title: "Day18"
date: 2021-04-19T21:57:49+08:00
lastmod: 2021-04-19
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### ![20210419193033](https://img.fengqigang.cn//img/20210419193033.png) 为什么要将 **FileOutputStream out = null;** 放在外面，可以放在 try 语句里面?

不可以


![20210419193142](https://img.fengqigang.cn//img/20210419193142.png)

放在 out 中， 其作用的域只能在 try  中， finally 中的 try 无法使用

### reader 的继承关系是什么样的?

![20210419193525](https://img.fengqigang.cn//img/20210419193525.png)

### **InputStreamReader** 的构造方法是什么样的?

![20210419193710](https://img.fengqigang.cn//img/20210419193710.png)

```java
public class CountNum {
    public static void main(String[] args) throws IOException {
        // 第一种构造方法
        InputStreamReader in = new InputStreamReader(new FileInputStream("a.txt"));

        // 第二种构造方法
        InputStreamReader input = new InputStreamReader(new FileInputStream("a.txt"), "GBK");
    }
}
```

### 如何使用 InputStreamReader 实现单个 char 的构造方法?

int

read()

Reads a single character.


```java
public class CountNum {
    public static void main(String[] args) throws IOException {
        InputStreamReader in = new InputStreamReader(new FileInputStream("a.txt"));

        // 单个
        int readData = in.read();
        System.out.println(((char) readData));

        // close
        in.close();
    }
}
```

### 如何使用 InputStreamReader 实现多个 char 的构造方法?

int 

read(char[] cbuff, int offset, int length)

Reads characters into a portion of an array.

```java
public class CountNum {
    public static void main(String[] args) throws IOException {
        InputStreamReader in = new InputStreamReader(new FileInputStream("a.txt"));

        // 多个
        char[] chars = new char[1024];
        int readCount = in.read(chars);
        System.out.println((new String(chars, 0, readCount)));

        // close
        in.close();
    }
}
```

###  如何使用 InputStreamReader 实现单字符边读边写?

public int read()

**Returns:**

The character read, or -1 if the end of the stream has been reached.

```java
public class CountNum {
    public static void main(String[] args) throws IOException {
        InputStreamReader in = new InputStreamReader(new FileInputStream("a.txt"));
        OutputStreamWriter out = new OutputStreamWriter(new FileOutputStream("bb.txt"));

        // 边读书边写
        int readData;
        while ((readData = in.read()) != -1) {
            out.write(readData);
        }

        // close
        in.close();
        out.close();
    }
}
```

### 如何用 **InputStreamReader** 实现多个字符边读边写?


public int read(char[] cbuff, int offset, int length)

**Returns:**

The number of characters read, or -1 if the end of the stream has been reached.


```java
public class CountNum {
    public static void main(String[] args) throws IOException {
        InputStreamReader in = new InputStreamReader(new FileInputStream("a.txt"));
        OutputStreamWriter out = new OutputStreamWriter(new FileOutputStream("b.txt"));

				// 多个字符的方式
        char[] chars = new char[1024];
        int readCount;
        while ((readCount = in.read(chars)) != -1) {
            out.write(chars, 0, readCount);
        }
    }
}
```

### ![20210419200409](https://img.fengqigang.cn//img/20210419200409.png) InputStreamReader 可以实现图片的复制吗? 为什么?

不可以

### InputStramReader 如何实现编码?

```java
public class CountNum {
    public static void main(String[] args) throws IOException {
        InputStreamReader in = new InputStreamReader(new FileInputStream("a.txt"), "GBK");

        char[] chars = new char[1024];

        int readCount = in.read(chars);
        System.out.println(new String(chars, 0, readCount));
    }
}
```

### FileWriter 是干什么的?

Convenience class for writing character files.

### 如何构造 **FileWriter**?

FileWriter (File file)

Constructs a FileWriter given the File to write, using the platform's default charset.

FileWriter (String fileName)

Constructs a FileWriter given a file name, using the platform's default charset.

```java
public class CountNum {
    public static void main(String[] args) throws IOException {
        // 第一种方式
        FileWriter fileWriter = new FileWriter(new File("a.txt"));

        // 第二种方式
        FileWriter fileWriter2 = new FileWriter("a.txt");
    }
}
```

### 如何用 fileWriter 向 a.txt 写 "什么是快乐星球?" ?

void write(String str, int off, int len)

Writes a portion of a string.

```java
public class CountNum {
    public static void main(String[] args) throws IOException {
        FileWriter fileWriter = new FileWriter("a.txt");

        String s = "什么是快乐星球?";
        fileWriter.write(s);
        fileWriter.close();
    }
}
```

### **FileReader** 是干什么的? 它的构造方法是什么?

public class FileReader

Reads txt from character files using a default buffer size.

![20210419202221](https://img.fengqigang.cn//img/20210419202221.png)

### 如何用 **FileReader** 创建一个字符文件输入流并读取数据?

```java
public class CountNum {
    public static void main(String[] args) throws IOException {
        FileReader reader = new FileReader("a.txt");

        char[] chars = new char[1024];
        int readCount = reader.read(chars);
        System.out.println(new String(chars, 0, readCount));

        reader.close();
    }
}
```

### 转化流 VS 简化流?

1. 转化流使用麻烦， **简化流使用相对简单**

2. 转化流可以显示的指定字符集(构造方法) 简化流没有办法指定字符集，**只能使用平台默认字符集**

### BufferWriter 的默认字节是多少?

![20210419203435](https://img.fengqigang.cn//img/20210419203435.png)

因为是 Char 类型，所以它的默认字节是16K

### BufferWriter 它的特殊方法是什么，如何使用?

void newLine()

Writes a line separator

```java
public class CountNum {
    public static void main(String[] args) throws IOException {
        BufferedWriter bw = new BufferedWriter(new FileWriter("a.txt"));
        bw.write("RNG夺冠");
        bw.newLine();
        bw.write("拉拉");
        bw.close();
    }
}
```

![20210419203913](https://img.fengqigang.cn//img/20210419203913.png)

### BufferReader 它的特殊方法是什么， 如何使用?

Public String readLine()

A String containing the contents of the line, not including any line0 termination characters, or null if the end of the stream has been reached without reading any characters.

```java
public class CountNum {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new FileReader("a.txt"));

        String s = br.readLine();
        System.out.println(s);
        String s2 = br.readLine();
        System.out.println(s2);
        String s3 = br.readLine();
        System.out.println(s3);
        br.close();
    }
}
```

![20210419204408](https://img.fengqigang.cn//img/20210419204408.png)

### 如何用![20210419204501](https://img.fengqigang.cn//img/20210419204501.png) while循环来做?

```java
public class CountNum {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new FileReader("a.txt"));

        String line;
        while ((line = br.readLine()) != null) {
            System.out.println(line);
        }
        br.close();
    }
}
```

![20210419204634](https://img.fengqigang.cn//img/20210419204634.png)

### 为什么会产生数据流?

```java
public class CountNum {
    public static void main(String[] args) throws IOException {
        FileOutputStream out = new FileOutputStream("a.txt");
        out.write(1000);
        out.write(3.14);
        out.close();
    }
}
```

在字符滻中无法满足 写入 1000, 3.14 这样的要求

没有通过字节流去写入 java 基本数据类型， 所以就有了数据流

### 如何通过 DataOutPutStream 写入 1000, 并通过 DataInputStream 读取 1000?

DataInputStream (OutInputStream out)

A data input stream lets an application read primitive Java data tyeps from an underlying input stream in a machine-independent way. An application uses a data output to write data that can later be read by a data input stream.

```java
public class CountNum {
    public static void main(String[] args) throws IOException {
        DataOutputStream out = new DataOutputStream(new FileOutputStream("a.txt"));
        DataInputStream in = new DataInputStream(new FileInputStream("a.txt"));

        out.writeInt(1000);
        out.close();

        int i = in.readInt();
        System.out.println(i);
    }
}
```

![20210419205627](https://img.fengqigang.cn//img/20210419205627.png)




### 在使用 DataOutputStream 与 DataInputStream 时需要注意什么?

什么样的顺序去写入，就需要按照相同的顺序去读取

![20210419205850](https://img.fengqigang.cn//img/20210419205850.png)

### 如何实现 PrintUtils 工具类, 有一个 OutputStream 成员， 可以实现写整数， 整数+换行， 浮点数, 浮点数+换行的功能?

```java
public class PrintUtils {
    public OutputStream out;

    // 构造方法
    public PrintUtils(OutputStream outputStream) {
        this.out = outputStream;
    }

    // 写整数
    public void printInt(int a) throws IOException {
        String s = String.valueOf(a);
        out.write(s.getBytes());
    }

    public void printLnInt(int a) throws IOException {
        String s = String.valueOf(a);
        out.write(s.getBytes());
        out.write(System.lineSeparator().getBytes());
    }

    public void printDouble(double d) throws IOException {
        String s = String.valueOf(d);
        out.write(s.getBytes());
    }

    public void printLnDouble(double d) throws IOException {
        String s = String.valueOf(d);
        out.write(s.getBytes());
        out.write(System.lineSeparator().getBytes());
    }


    public void close() throws IOException {
        out.close();
    }
}
```

```java
public class Demo3 {
    public static void main(String[] args) throws IOException {
        PrintUtils printUtils = new PrintUtils(new FileOutputStream("a.txt"));
        printUtils.printInt(10000);

        // close
        printUtils.close();
    }
}
```

### 打印流是怎么分类的?

PrintStream 字节打印流

PrintWriter 字符打印流

### PrintWriter 是如何实现自动刷新的?

PrintWriter (Writer out, boolean autoFlush)

Creates a new PrintWriter

autoFlush - A boolean:

if true, the println, printf, or format methods will flush the output buffer.

### 什么是标准输入流与标准输出流?

标准输出流 System.out 默认的输出设备是 **显示器**

是一个字节打印流

标准输入流 System.in 默认的输入设备是 **键盘**

是普通的字节输入流

```java
public class Demo3 {
    public static void main(String[] args) throws IOException {
        InputStream in = System.in;

        PrintStream out = System.out;
    }
}
```

### 如何用 BufferedReader 实现 Scanner 的功能?

```java
public class Demo3 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        String line;
        while ((line = br.readLine()) != null) {
            if (line.equals("88")) {
                break;
            }
        }
        br.close();
    }
}
```

![20210419212245](https://img.fengqigang.cn//img/20210419212245.png)

### 对象流中有哪些分类?

ObjectOutPutStream 序列化流

ObjectInputStream 反序列化流

### 什么是会有对象流?

需要将 对象 给存储起来

```java
Student student = new Student("张三", 18);
// 通过序列化流， 把这个学生对象给存储起来
// 通过反序列化流去 把这个学生对象给还原回来
```

### 如何创建序列化流(student ("小五", 18))，并写入文件中(a.txt) 中?

```java
public class Demo3 {
    public static void main(String[] args) throws IOException {
        // 创建学生对象
        Student student = new Student("小五", 18);

        // 创建序列化流
        ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("a.txt"));

        // 写对象
        out.writeObject(student);
        out.close();
    }
}

class Student {
    String name;
    int age;

    public Student(String name, int i) {
        this.name = name;
        this.age = age;
    }
}
```

![20210419213609](https://img.fengqigang.cn//img/20210419213609.png)

实现Serializable接口, 它是个空标记，无需进行重写

```java
public class Demo3 {
    public static void main(String[] args) throws IOException {
        // 创建学生对象
        Student student = new Student("小五", 18);

        // 创建序列化流
        ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("a.txt"));

        // 写对象
        out.writeObject(student);
        out.close();
    }
}

class Student implements Serializable{
    String name;
    int age;

    public Student(String name, int i) {
        this.name = name;
        this.age = age;
    }
}
```

### 如何实现反序列化，强行匹配(a.txt, Student)?

static final long serivalVersionUID = xxxxxxxl;

```java
public class Demo3 {
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        ObjectInputStream in = new ObjectInputStream(new FileInputStream("a.txt"));

        Student student = (Student) in.readObject();
        System.out.println(student);
    }
}

class Student implements Serializable {
    String name;
    int age;
    static final long serialVersionUID = -7120293785956270919l;


    public Student(String name, int i) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

![20210419214148](https://img.fengqigang.cn//img/20210419214148.png)


### 有什么方法让某些成员变量拒绝序列化，只会赋默认值?

transient

![20210419214408](https://img.fengqigang.cn//img/20210419214408.png)

### 在**java** IO 中有什么类型的流?

基类

文件相关

缓冲相关

转换流

数据流

对象流

### 在**java** IO 中有基类有哪些流?

**字节**:

1. 输出 OutputStream

2. 输入 InputStream

**字符**:

1. 输出 Writer

2. 输入 Reader

### 在**java** IO 中有哪些文件相关的流?

**字节**:

1. 输出 FileOutputStream

2. 输入 FileInputStream

**字符**:

1. 输出 FileReader

2. 输入 FileWriter

### 在**java** IO 中有哪些缓冲相关的流?

**字节**

1. 输出 BufferedOutputStream

2. 输入 BUfferedInputStream

**字符**

1. 输出 BufferWriter

2. 输入 BufferedReader

### 在 **java** IO 中有哪些字符转换流?

**无字节输出流和字节输入流**

**字符输出流**

OutputStreamWriter

**字符输入流**

InputStreamReader

### 在 **java** IO 中有哪些数据流?

**无字符输出流和字符输入流**

**字节输出流**

DataOutputStream

**字节输入流**

DataInputStream

### 在 **java** IO 中有哪些打印流?

**无字节输入流 和 字符输入流**

**字节输出流**

PrintStream

**字符输出流**

PrintWriter

### 在 **java** IO 中有哪些对象流?

**无字符输出流和字符输入流**

**字节输出流**

ObjectOutPutStream

**字节输出流**

ObjectInputStream

