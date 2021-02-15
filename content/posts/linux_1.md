---
title: "Linux_1"
date: 2021-02-15T21:57:09+08:00
lastmod: 2021-02-15
author: "xiaonan"
math:
 enable: true

tags: [linux]
categories: [鸟哥的私房菜]
---

# 电脑: 辅助人脑的好工具
## 计算机硬件的五大单元
### 计算机硬件有哪五大单元？
1. 输入单元
2. 输出单元
3. 控制单元
4. 算数逻辑单元
5. 存储单元

![](https://img.fengqigang.cn//img/20210215152517.png)

### cpu中包含哪些单元？

控制、算术逻辑单元

![](https://img.fengqigang.cn//img/20210215152831.png)

### CPU-什么是CPU的架构？

首先，使用软件都需要经过CPU内部的微指令集来达成才行。其次，这些指令集的设计主要被分为两种设计理念，也就是两种主要的CPU架构: 分别为:精简指令集(RISC)与复杂指令集(CISC)系统。

### CPU-什么是精简指令集(RISC)？

RISC 即 Reduced Instruction Set Computer.

其特点是:
- 每个指令的执行时间很短
- 完成的动作单纯
- 指令的执行性能较佳
- 若做复杂的事情，需要多个指令来完成

其应用：
- 甲骨文的SPARC CPU
	- 学术领域的大型工作站
	- 银行金融体系的主要服务器
- IBM的Power Architecture
	- 索尼的Play Station 3
- 安谋(ARM Holdings)的ARM CPU
	- 手机
	- PDA(Personaldigital assistant)
	- 导航系统
	- 网络设备(交换器、路由器)

### CPU-什么是复杂指令集(CISC)?

CISC 即 Complex Instruction Set Computer.

其特点是:
- 每个微指令集可又执行一些较低阶的硬件操作
- 指令数目多而且复杂
- 每条指令的长度并不相同

### CPU-所谓的x86架构是如何而来的？

因为最早的Intel发展出来的CPU代号称为8086, 后来依此架构以开发出80286, 80386..., 因此这种架构的CPU就被称为x86架构

### CPU-所谓的x86_64中的64指的是什么？

64CPU代表CPU一次可以读写64bits这么多的数据

#### 64bits有多大？

即2的64方

### CPU-如何在linux下查看当前CPU所支持的指令集？

```bash
cat /proc/cpuinfo
```

![](https://img.fengqigang.cn//img/20210215163221.png)

### 容量单位-计算中的容量单位有哪些？它们如何进行转化？

文件大小使用的是`二进制`的方式

|进位制 |Kilo |Mega |Giga |Tera |Peta | exta| Zetta |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|二进制 | 1024|1024K | 1024M|1024G|1024T|1024P|1024E|
| 十进制| 1000|1000K|1000M|1000G|1000T|1000P|1000E|

### 容量单位-假设你今天购买了500GB的硬盘一颗，但是格式化完毕后却剩下460GB左右的容量，这是什么原因?

因为一般的硬盘制造商会使用`十进制`的单位

500GByte 代表为 500 * 1000 * 1000 * 1000 Byte
转成文件的容量单位时使用二进制(1024为底)，所以就成466GB左右容量

### 速度单位-计算中的速度单位有哪些？它们如何进行转化？

CPU的运算速度常用`MHZ`或者是`GHZ`

网络常使用的单位为`Mbps`即`Mbits per second`


|进位制 |Kilo |Mega |Giga |Tera |Peta | exta| Zetta |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|二进制 | 1024|1024K | 1024M|1024G|1024T|1024P|1024E|
| 十进制| 1000|1000K|1000M|1000G|1000T|1000P|1000E|


### 速度单位-20M/5M传输速度，如果转成文件大小的Byte时，其实理论最大传输为多少？

网络常使用的单位为`Mbps`即`Mbits per second`

其实理论最大的传输值为 每秒2.5MByte/每秒625KByte的下载/上传速度




