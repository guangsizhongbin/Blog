---
title: "Day22"
date: 2021-04-23T23:14:11+08:00
lastmod: 2021-04-23
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

###   什么是计算机网络

1.  物理互联
    
2.  软件支持
    
3.  目的: 资源共享 \+ 信息传递
    

### 什么是网络编程?

处于 **互联网络** 上不同计算机 **程序间** 的数据交换

### OSI参考模型有几层? 分别是什么?

**7 层**

物理层

数据链路层

网络层

传输层

会话层

表示层

应用层

**物联网淑惠试用**

### 物理层主要关注什么?

关注一条通信信道上传输原始比特(01)

其功能是确保当一方发送了比特1, 另一方收到的是比特1, 而不是0

### 物理层的所涉及到的典型问题是什么?

1.  用什么样的电信号表示0和1
    
2.  一个 bit 持续多少纳秒
    
3.  传输是否可以在两个方向同时进行
    
4.  初始连接如何建立，传输结束后之后如何撤销连接
    

**规定一个特殊的电信号将普通的数据信号分开来**

### 数据链路层主要关注什么?

将一个原始的传输设施转变成一条 **没有漏检传输错误** 的传输线路

**检查数据是否发生差错**

### 数据链路层的主要功能是什么?

1.  成帧

![20210421210322](https://img.fengqigang.cn//img/20210421210322.png)

2.  差错控制(帧校验，确认 \+ 超时重传)
    
3.  流量控制
    
4.  广播式网络的数据链路层, 还有介质访问控制问题
    

**介质访问控制**

![20210421211910](https://img.fengqigang.cn//img/20210421211910.png)

保证只有一台计算机在发送数据

### 网络层需要解决的核心功能是什么?

如何将数据包从源端路由到接收端

### 什么是端到端的通信?

应用程序所对应的 **进程间** 的通信

### 什么是端口?

整数值

在一台主机中代表一个唯一的进程标志

### 传输层主要考虑的是什么?

向上层提供端到端的通信服务，屏蔽底层的通信细节

### 传输层有哪些功能?

1.  提供应用进程之间的逻辑通信
    
2.  复用和分用
    

![20210421213305](https://img.fengqigang.cn//img/20210421213305.png)

3.  向上层提供不同类型的通信服务

**TCP** , **UDP**

### 什么 **TCP** 协议?

面向连接的可靠的通信服务（如: 打电话）

**Transmission Control Protocol**

![](https://img.fengqigang.cn//img/20210423111320.png)

### 什么 **UDP** 协议?

无连接的不可靠的通信服务(如: 写信)

**User Datagram Protocol**

![](https://img.fengqigang.cn//img/20210423111125.png)

### 若要使用 **UDP** 协议进行传输，有哪几步?

**发送端**

1.  建立 udp 的 socket 对象
    
2.  将要发送的数据封装成数据包
    
3.  通过 udp 的 socket 对象， 将数据包发送出
    
4.  释放资源
    

**接收端**

1.  建立 udp 的 socket 对象
2.  创建用于接收数据的数据报包，通过 socket 对象的 receive 方法接收数据
3.  通过数据包对象的功能来完成对接受到数据进行解析
4.  可以对资源进行释放

### 若要使用 TCP 协议进行传输，有哪几步?

**客户端**

1.  建立客户端的 Socket 服务， 并明确要连接的服务器
2.  如果对象建立成功，就表明已经建立了数据传输的通道，就可以在该通道通过IO进行数据的读取和写入
3.  根据需要从socket对象中获取输入, 或输出流
4.  向流中读取或写入数据， 释放资源

**(接受端)服务端**

1. 创建 Serversocket 对象， 在指定端口，监听客户端连接请求
2. 收到客户端连接请求后，建立Socket连接
3. 如果连接建立成功，就表明已经 了数据传输的通道，就可以在该通道通过IO进行数据的读取和写入
4. 从 socket 中根据需要获取输入，或输出流，根据需要向流中写入数据或从流中读数据，释放资源



![](https://img.fengqigang.cn//img/20210423171954.png)

### 如何实现客户端(tcp) socket?

public class Socket
extends Object
implements Closeable

This class implements client sockets (also called just "sockets"). A socket is an endpoint for communication between two machines.

**Constructor**

Socket(String host, int port)
Creates a stream socket and connects it to the specified port number on the named host.

**Method**

InputStream getInputStream()
Returns an input stream for this socket.

OutputStream getOutputStream()
Returns an output stream for this socket.

```java
public class Client {
    public static void main(String[] args) throws IOException {
        // 建立客户端的 Socket 服务， 并明确要连接服务器
        // Socket(String host, int port)
        Socket socket = new Socket("127.0.0.1", 8888);
        // 如果对象建立成功，就表明已经建立了数据传输的通道
        // 就可以在该通道通过IO进行数据的读取和写入
        // 想服务端发送数据
        OutputStream out = socket.getOutputStream();
        out.write("Hello tcp".getBytes());
        // 释放资源
        socket.close();
    }
}
```

### 如何实现接受端(Tcp) socket?

public class ServerSocket
extends Object
implements Closeable

This class implements server sockets. A server socket waits for requests to come in over the network. It performs some operation based on that request, and then possibly returns a result to the requester.

**Construct**

ServerSocket(int port)
Creates a server socket, bound to the specified port.

**method**

Socket accept()
Listens for a connection to be made to this socket and accepts it.

```java
public class Server {
    public static void main(String[] args) throws IOException {
       // 创建 ServerSocket 对象， 在指定端口，监听客户端连接请求
        ServerSocket serverSocket = new ServerSocket(8888);
        // 收到客户端连接请求后，建立socket连接
        Socket socket = serverSocket.accept();
        // 从 socket 中根据需要获取输入，或输出流
        InputStream in = socket.getInputStream();
        // 解析数据
        byte[] bytes = new byte[1024];
        int readCount = in.read(bytes);
        String s = new String(bytes, 0, readCount);
        System.out.println(s);
        
        socket.close();
        serverSocket.close();
    }
}
```

**先运行服务端**

### 如何实现TCP, 客户端发送数据，服务端给予反馈?

**Client**

```java
public class Client {
    public static void main(String[] args) throws IOException {
        // 建立客户端 Socket 服务， 并明确要连接的服务器
        Socket socket = new Socket("127.0.0.1", 8888);
        // 如果对象建立成功，就表明已经建立了数据传输的通道
        // 向服务端发送数据
        OutputStream out = socket.getOutputStream();
        out.write("hello tcp".getBytes());

        // 接受来自客户端的反馈
        // 获取输入流
        InputStream in = socket.getInputStream();
        byte[] bytes = new byte[1024];
        int readCount = in.read(bytes);
        String s = new String(bytes, 0, readCount);
        System.out.println(s);

        // 释放资源
        socket.close();
    }
}
```

**Server**

```java
public class Server {
    public static void main(String[] args) throws IOException {
        // 创建 Serversocket 对象， 在指定端口，监听客户端连接请求
        ServerSocket serverSocket = new ServerSocket(8888);
        // 收到客户端连接请求后， 建立 socket 连接
        Socket socket = serverSocket.accept();
        // 从 socket 中根据需要获取输入，或输出流
        InputStream in = socket.getInputStream();

        // 解析数据
        byte[] bytes = new byte[1024];
        int readCount = in.read(bytes);
        String s = new String(bytes, 0, readCount);
        System.out.println(s);

        // 给客户端一个反馈信息
        OutputStream out = socket.getOutputStream();
        out.write("好你妹".getBytes());

        socket.close();
        serverSocket.close();
    }
}
```

![image-20210423192929605](C:%5CUsers%5Cfeng%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20210423192929605.png)

### 如何把客户端文件上传到服务器?

**Client**

1.  创建 Socket 对象
2.  读取本地文件
3.  获取输出流

```java
public class Client {
    public static void main(String[] args) throws IOException {
        // 创建 Socket 对象
        Socket socket = new Socket("127.0.0.1", 11111);

        // 读取本地文件
        FileInputStream in = new FileInputStream("a.txt");

        // 获取输出流
        OutputStream out = socket.getOutputStream();
        byte[] bytes = new byte[1024];
        int readCount;
        while ((readCount = in.read(bytes)) != -1) {
            out.write(bytes, 0, readCount);
        }
        in.close();
        socket.close();
    }
}
```

**Server**

1.  创建输出流对象， 写入服务器

```java
public class Server {
    public static void main(String[] args) throws IOException {
        ServerSocket serverSocket = new ServerSocket(11111);
        Socket socket = serverSocket.accept();

        // 创建输出流对象
        FileOutputStream out = new FileOutputStream("b.txt");
        InputStream in = socket.getInputStream();

        // 写入服务器
        int readCount;
        byte[] bytes = new byte[1024];
        while ((readCount = in.read(bytes)) != -1) {
            out.write(bytes, 0, readCount);
        }

        // 关闭流
        out.close();
        socket.close();
        serverSocket.close();
    }
}
```

### 如何实现 DatagramSocket(udp) 发送端?

public class **DatagramSocket**
extends Object
implements Closeable
This class represents a socket for sending and receiving datagram packets.

public final class **DatagramPacket**
extends Object
This class represents a datagram packet.

**constructor** ：

DatagramSocket(int port)
Constructs a datagram socket and binds it to the specified port on the local host machine.

**method**

void send(DatagramPacket p)
Sends a datagram packet from this socket.

DatagramPacket(byte\[\] buf, int offset, int length, InetAddress address, int port)
Constructs a datagram packet for sending packets of length length with offset ioffsetto the specified port number on the specified host.

**发送端**

```java
public class Sender {
    public static void main(String[] args) throws IOException {
        // 1. 将立 udp 的 socket 对象
        DatagramSocket datagramSocket = new DatagramSocket(8888);

        // 2. 将要发送的数据封装成数据包
        String s = "hello udp";
        byte[] bytes = s.getBytes();
        InetAddress targetIP = InetAddress.getByName("127.0.0.1");
        int port = 9999;
        DatagramPacket packet = new DatagramPacket(bytes, 0, bytes.length, targetIP, port);

        // 3. 将数据包发送出
        datagramSocket.send(packet);

        // 4. 释放资源
        datagramSocket.close();
    }
}
```

### 如何实现 DatagramSocket(udp) 接受端?

public class **DatagramSocket**
extends Object
implements Closeable
This class represents a socket for sending and receiving datagram packets.

public final class **DatagramPacket**
extends Object
This class represents a datagram packet.

**method**

DatagramPacket(byte\[\] buf, int offset, int length)
Constructs a DatagramPacket for receiving packets of length length, specifying an offset into the buffer.

void receive(DatagramPacket p)
Receives a datagram packet from this socket.

```java
public class Receiver {
    public static void main(String[] args) throws IOException {
        // 1. 建立 udp 的 socket 对象
        DatagramSocket datagramSocket = new DatagramSocket(9999);

        // 2. 创建用于接收数据的数据报包，通过 socket 对象的 receive 方法接收数据
        byte[] bytes = new byte[1024];
        DatagramPacket packet = new DatagramPacket(bytes, 0, bytes.length);
        datagramSocket.receive(packet);

        // 3. 通过数据包对象的功能来完成对接受到数据进行解析 
        byte[] data = packet.getData();
        int offset = packet.getOffset();
        int length = packet.getLength();
        String s = new String(data, offset, length);
        System.out.println(s);

        // 4. 对资源进行释放
        datagramSocket.close();


    }
}
```

### 接受端与发送端的工具类实现?

```java
public class NetworkUtils {
    public static DatagramPacket getSenderPacket(String targetIp, int port, String message) throws UnknownHostException {
        // 创建用于发送的数据报包
        byte[] bytes = message.getBytes();
        InetAddress ip = InetAddress.getByName(targetIp);
        DatagramPacket packet = new DatagramPacket(bytes, 0, bytes.length, ip, port);
        return packet;
    }

    // 创建用于接受的数据报包
    public static DatagramPacket getReceiverPacket() {
        byte[] bytes = new byte[1024];
        DatagramPacket packet = new DatagramPacket(bytes, 0, bytes.length);
        return packet;
    }

    // 解析数据
    public static String parsePacket(DatagramPacket packet) {
        byte[] data = packet.getData();
        int offset = packet.getOffset();
        int length = packet.getLength();
        String s = new String(data, offset, length);
        return s;
    }
}
```

![](https://img.fengqigang.cn//img/20210423144905.png)

![](https://img.fengqigang.cn//img/20210423144958.png)

### 接受端与发送端都可发送和接受数据?

- 发送端

**发送** 和 **接收**

![](https://img.fengqigang.cn//img/20210423145721.png)

**退出条件**

![](https://img.fengqigang.cn//img/20210423145807.png)

- 接受端

![](https://img.fengqigang.cn//img/20210423150244.png)

### 会话层主要功能是什么?

记录谁发了消息，记录检查点

### 表示层主要功能是什么?

处理两个通信系统中交换信息的表示方式

编码和表示方法

数据是否压缩，数据的加密和解密使用何种加密算法

### 应用层主要功能是什么?

包含了用户通常所需要的各种协议

Http协议

### IP地址是怎么组成的?

网络号码 \+ 主机地址(唯一的)

### A类， B类， C类, D类, E类,IP地址是如何分类的?

A类:

第一段号码为网络号码， 剩下的三段号码为本地计算机的号码

B类:

前二段号码为网络号码， 剩下的二段号码为本地计算机的号码

C类:

前三段号码为网络号码， 剩下的一段号码为本地计算机的号码

D类:

(组播的目的地址)

E类:

(保留地址)

### 什么是网络地址，广播地址?

对于A, B, C 不同类型的网络地址，都包含两个特殊的ip地址

网络地址:

表示该类网络本身

xxx.xxx.xxx.0

广播地址:

代表的是当前这个网络中，所有的主机

xxx.xxx.xxx.255

### 哪个是回环地址?

127.0.0.1

用于测试本机的网络是否有问题

### 两个主机之间通信的原理图是什么样的?

![](https://img.fengqigang.cn//img/20210423110750.png)

### **config.properties** (key-value)一般用于存储哪些东西?

- 数据库配置
    - 开发数据库
    - 测试数据库
    - 线上数据库(生产环境)
- 第三方配置信息
    - APP Key

### 如何读取 **config.properties**?

public class Properties
extends Hashtable&lt;Object,Object&gt;
The Properties class represents a persistent set of properties. The Properties can be saved to a stream or loaded from a stream. Each key and its corresponding value in the property list is a string.

**Constructors**

Properties()
Creates an empty property list with no default values.

**Method**

void load(InputStream inStream)
Reads a property list (key and element pairs) from the input byte stream.

void load(Reader reader)
Reads a property list (key and element pairs) from the input character stream in a simple line-oriented format.

String getProperty(String key)
Searches for the property with the specified key in this property list.

![](https://img.fengqigang.cn//img/20210423160401.png)

### 如何读取 **config.properties**(实现编码一致)?

public class Properties
extends Hashtable<Object,Object>

The Properties class represents a persistent set of properties. The Properties can be saved to a stream or loaded from a stream. Each key and its corresponding value in the property list is a string.



void	load(InputStream inStream)
Reads a property list (key and element pairs) from the input byte stream.



String	getProperty(String key)
Searches for the property with the specified key in this property list.

```java
public class Demo2 {
    public static void main(String[] args) throws IOException {
        Properties properties = new Properties();
        properties.load(new InputStreamReader(new FileInputStream("config.properties"), "GBK"));
        String user = properties.getProperty("user");
        System.out.println(user);
    }
}
```





### 实现自动回复的机器人?

1.  Sender
    
2.  Receiver

