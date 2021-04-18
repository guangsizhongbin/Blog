---
title: "Day17"
date: 2021-04-18T23:19:15+08:00
lastmod: 2021-04-18
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

###   如何实现对 **FilterInput** 实现装饰器模式, 对接收到的字母转换成小写?

```java
public class Demo {
    public static void main(String[] args) throws IOException {
        // 方法一:
        BufferedInputStream br = new BufferedInputStream(new FileInputStream("a.txt"));
        LowerCaseInputStream lowerCaseInputStream = new LowerCaseInputStream(br);

        // 方法二:
       new LowerCaseInputStream(new BufferedInputStream(new FileInputStream("a.txt")));

        // 单字节
        int readData = lowerCaseInputStream.read();
        System.out.println((char)readData);

        // 字节数组
        byte[] bytes = new byte[1024];
        int readCount = lowerCaseInputStream.read(bytes, 0, bytes.length);
        System.out.println(new String(bytes, 0, readCount));
        lowerCaseInputStream.close();

    }
}

class LowerCaseInputStream extends FilterInputStream{

    /**
     * Creates a <code>FilterInputStream</code>
     * by assigning the  argument <code>in</code>
     * to the field <code>this.in</code> so as
     * to remember it for later use.
     *
     * @param in the underlying input stream, or <code>null</code> if
     *           this instance is to be created without an underlying stream.
     */
    protected LowerCaseInputStream(InputStream in) {
        super(in);
    }

    @Override
    public int read() throws IOException {
       int read = super.read();
       int read1 = (char) read;
        int c = Character.toLowerCase(read1);
        return c;
    }

    @Override
    public int read(byte[] b, int off, int len) throws IOException {
        int readCount = super.read(b, off, len);
        for (int i = off; i < off + readCount; i++) {
            b[i] = ((byte) Character.toLowerCase((char) b[i]));
        }

        return readCount;
    }
}
```

### 创建字节数组和单字节IO模式是什么样的?

**单字节**

```java
public class CountNum {
    public static void main(String[] args) throws IOException {
        // 创建输入流对象
        FileInputStream in = new FileInputStream("a.txt");
        // 读数据
        int readData;
        while ((readData = in.read()) != -1) {
            System.out.println((char) readData);
        }
        in.close();
    }
}
```

**字节数组**

```java
public class CountNum {
    public static void main(String[] args) throws IOException {
        // 创建输入流对象
        FileInputStream in = new FileInputStream("a.txt");
        // 读数据
        byte[] bytes = new byte[12];
        int readCount;
        while ((readCount = in.read(bytes)) != -1) {
            System.out.println(new String(bytes, 0, readCount));
        }
        in.close();
    }
}
```

### 什么会有字符流?

1.  用字节流读取英文字符与数字

没有问题 能够正常显示

2.  用字节流读取中文字符

可能会有问题

### 一个字符在计算机当中是怎样存储的?

基于某个编码表，有与这对应的整数值(编码值)存储在计算机当中的

### 什么是编码?

基于某个编码表，把字符数据转化成编码值的过程

### 什么是解码?

基于某个编码表，把编码值转化成字符数据的过程

### 什么是 ASCII 表?

美国标准信息交换码

用一个字节的7位可表示，128

### 什么 ISO8859-1 码表?

拉丁码表，欧洲码表

用一个字节的8位表示

0000 0000 - 1111 1111

### 什么是 GB 码表?

GB2312

中国的中文编码表

GBK

中国的中文编码表升级， 融合了更多的中文文字符号

GB18030

GBK的取代版本

BIG-5码

通行于台湾，香港地区的一个繁体它编码方案，俗称 "大五码"

### UTF-8 是什么样的?

是用可变长度来表示一个字符

UTF-8, 字定义一种 "区间规则", 这种规则可以和 ASCII 编码保持最大程序的兼容

1字节 0xxxxxxx

2字节 110xxxxx 10xxxxxx

3字节 1110xxxx 10xxxxxx 10xxxxxxx

### 如何获取 idea 默认的字符集?

```java
public class CountNum {
    public static void main(String[] args) throws IOException {
        Charset charset = Charset.defaultCharset();
        System.out.println(charset);
    }
}
```

![20210418210102](https://img.fengqigang.cn//img/20210418210102.png)

### 字符流的本质是什么?

字节流 \+ 编码表

![20210418210538](https://img.fengqigang.cn//img/20210418210538.png)

### 如何实现字符的编码与解码?

1.  编码

getBytes(String charsetName)

2.  解码

String(byte\[\] bytes, String charsetName)

```java
public class CountNum {
    public static void main(String[] args) throws IOException {
        String s = "你好";

       // 编码
        byte[] utf8Encoding = s.getBytes();
        System.out.println(Arrays.toString(utf8Encoding));

        // 解码
        String s2 = new String(utf8Encoding);
        System.out.println(s2);
    }
}
```

### OutputStreamWriter 充当的是什么的角色? 如何使用?

An OutputStreamWriter is a bridge from character streams to byte streams.

```java
public class CountNum {
    public static void main(String[] args) throws IOException {
        // 第一种构造方法
        FileOutputStream fileOutputStream = new FileOutputStream("a.txt");
        OutputStreamWriter out = new OutputStreamWriter(fileOutputStream);

        // 第二种方法
        OutputStreamWriter outputStreamWriter = new OutputStreamWriter(new FileOutputStream("a.txt"));

    }
}
```

### OutputStreamWriter 如何实现写单个字符与字符数组?

```java
public class CountNum {
    public static void main(String[] args) throws IOException {
        // 定义字符串
        String s = "我要为你写65页ppt";

        // 创建转换输出流对象
        OutputStreamWriter out = new OutputStreamWriter(new FileOutputStream("a.txt"));

        // 写单个字符
        writeSingle(s, out);

        // 写字符数组
        writeMulti(s, out);

        out.write(s);

        out.flush();
        out.close();
    }

    private static void writeMulti(String s, OutputStreamWriter out) throws IOException {
        char[] chars = s.toCharArray();
        out.write(chars);
    }

    private static void writeSingle(String s, OutputStreamWriter out) throws IOException {
        char[] chars = s.toCharArray();
        for (int i = 0; i < chars.length; i++) {
            out.write(chars[i]);
        }
    }

}
```


