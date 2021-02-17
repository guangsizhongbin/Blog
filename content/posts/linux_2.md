---
title: "Linux_2"
date: 2021-02-16T22:07:36+08:00
lastmod: 2021-02-16
author: "xiaonan"
math:
 enable: true

tags: [linux]
categories: [鸟哥的私房菜]
---

# 个人电脑架构与相关设备元件
## Intel芯片架构
### Intel芯片架构-什么是南北桥?它们是干什么的？[^南桥与北桥]
[^南桥与北桥]: [南北桥架构的演变](https://my.oschina.net/u/914655/blog/338903)

`北桥`: 负责链接速度较快的元件(在目前的主流架构中，大多将北桥内存控制器整合到CPU封装中了)
- CPU

- 内存

- 显卡接口等

`南桥`: 负责链接速度较慢的元件

- 硬盘

- USB

- 网卡

![](https://img.fengqigang.cn//img/20210216205121.png)

### Intel芯片架构-为什么现在的主流架构中，要将北桥内存控制器整合到CPU中？

首先, 北桥是负责链接速度较快的元件(内存), 然后，若CPU需要与内存交流，就需要经过北桥，这样就会瓜分掉北桥的总可用带宽，影响其他元件的沟通。最后，若将内存控制器整合到CPU后，CPU与内存之间的沟通是直接交流，速度较快，而且消耗更多的带宽。

### Intel芯片架构-什么是CPU的频率？[^CPUZ]
[^CPUZ]: [CPU-Z的参数怎么看 CPU-Z检测CPU型号全面解析](http://www.lotpc.com/yjzs/4626.html)

即CPU每秒钟可以进行的工作次数

速度单位使用的是`十进制`

![](https://img.fengqigang.cn//img/20210216210114.png)

即$3.5 \times 10 ^ 9$MHz

### Intel芯片架构-什么是CPU的外频与倍频？什么会有外频和倍频出现？

外频: CPU与外部元件进行数据传输时的速度

倍频: CPU内部用来加速工作性能的一个倍数

首先，所有的设备都得通过北桥来链接，因此每个设备的工作频率都应该相同。然后，CPU的运算速度应比其他设备要快，所以厂商会在
CPU内部进行加速。


![](https://img.fengqigang.cn//img/20210216205121.png)

### Intel芯片架构-如何查看计算机的外频与倍频？

![](https://img.fengqigang.cn//img/20210216212320.png)

![](https://img.fengqigang.cn//img/20210216212441.png)

即总线速度为外频

核心速度 = 倍频 x 总线速度

### Intel芯片架构-超频指的是超什么频？

![](https://img.fengqigang.cn//img/20210216213049.png)

首先，超频是指超外频, 在以前所有的数据都需要通过北桥，但是北桥不可能比CPU快，成为系统性能的瓶颈。其次，在新的CPU设计中，将北桥的功能整合到CPU内，使得CPU直接与内存、显卡进行沟通，CPU的频率设计就不需要考虑外频了，只需要考虑整体的频率。最后，现在的CPU-z中，外频变成100MHZ而倍频可以到30以上。

### Intel芯片架构-前端总线速度是什么？

前端总线速度(Front Side Bus)

CPU中的所有数据都是由内存提供的

查看内存信息

```bash
sudo dmidecode -t memory
```

![](https://img.fengqigang.cn//img/20210216214527.png)

**MT/s 与 MHz有什么关系?**[^MT/s与MHz？]
[^MT/s与MHz？]: [MT/s=MHz?](https://linustechtips.com/topic/462465-mts-mhz/)

等价

![](https://img.fengqigang.cn//img/20210216215343.png)

CPU可能从内存中取得的最快带宽是2400 MHz x 64 bit = 2400 MHz 8 Bytes = 19.2GB/s

![](https://img.fengqigang.cn//img/20210216220455.png)

### Intel芯片架构-什么是CPU字组大小?[^对2^32]
[^对2^32]: [32位CPU最多支持4G内存是怎么算出来的？（解惑篇）](https://blog.csdn.net/liujianyangbj/article/details/108074167)

CPU每次能够处理的数据量称为字组大小(word size)

32位的CPU最多支持最大到4GBytes

**如何计算？**

首先, CPU计算的时候不能直接访问硬盘的数据，但是可以直接访问内存里的数据。其次，32位的CPU是指它能寻找到$2^32$个地址，不是存储空间有多大。最后，若一个地址单元为8位，则32位的CPU最多为4GBytes.

$2^{32}$个地址 = $2^{32} \times 8 / 8$ Byte = $2^{22}$ KByte = $2^{12}$ MByte = $2^2$GB = $4$GB


### Intel芯片架构-什么是CPU的超线程?

超线程 Hyper-Threading, HT

线程是操作系统进行运算调动的最小单位, 它被包含在进程之中，是进程中实际运作单位，一个进程中可又并发多个线程。

超线程技术是把一个物理处理器在软件层变成两个逻辑处理器，可以使处理器在某一时刻，同步并行处理更多指令数据。

超线程是一种将CPU内部暂时闲置处理资源充分"调动"起来的技术，在多加入一个逻辑处理单元 ，这让CPU可以同时执行多个程序而共享一颗CPU内的资源，当两个线程都同时需要某一个资源时，其中一个要暂时停止，并让出资源，直到这些资源闲置后才能继续。


## 内存
### 内存-什么是动态随机存取内存？

动态随机存取内存: Dynamic Random Access Memory, DRAM

只有在通电时才能记录与使用，断电后数据就消失，因此也称这种RAM为挥发性内存

### 内存-什么是SDRAM与DDR SDRAM?

DDR 是所谓的双倍数据传送速度(Double Data Rate)

![](https://img.fengqigang.cn//img/20210217110832.png)

### 内存-什么是多通道设计?

传统的总线宽度一般大约为64位，为了要加大这个宽度，因此芯片组厂商就将两个内存汇总在一起，如果一支内存可达64位，两支内存可达到128位了

![](https://img.fengqigang.cn//img/20210217111300.png)

两支内存最好容量大小，型号也最好相同

### 内存-什么是DRAM与SRAM?

动态随机存取内存: Dynamic Random Access Memory, DRAM

静态随机存取内存: Static Random Access Memory, SRAM

![](https://img.fengqigang.cn//img/20210217111630.png)

L2 cache即采用的是SRAM设计，L2内存速度必须要与CPU频率相同，在设计上使用的电晶体较多，且价格较高，且L2内存速度必须要与CPU频率相同，在设计上使用的电晶体较多，价格较高，且不易做成大容量

### 内存-什么是ROM?

只读存储器: Read Only Memory, ROM

ROM是一种非挥发性的内存

BIOS(Basic Input Output System)是一套程序，这套程序是写死到主板上面的一个内存芯片中，这个内存芯片在没有通电时也能够将数据记录下来。

## 显卡
### 显卡-假设你的桌面使用1024x768分辨率，且使用全彩色(每个像素占用3Bytes的容量), 请问你的显卡至少需要多少内存才能使用这样的彩度？

1024 x 768 x 3 Bytes = 2.359296 MBytes

![](https://img.fengqigang.cn//img/20210217113015.png)

## 硬盘与存储设备
### 对于机械硬盘，它的扇区，磁道，柱面都要什么？[^Vol072]
[^Vol072]: [Vol 072 你的硬盘是如何储存数据的？](https://www.youtube.com/watch?v=svhIPM2VT8U&ab_channel=%E5%9B%9E%E5%BD%A2%E9%92%88PaperClip)

磁道(track): 即不同大小的同心圆
![](https://img.fengqigang.cn//img/20210217211606.png)


扇区(sector): 磁盘存储数据最小的数据块
	- 因为同心圆外圈的圆比较大，占用的面积比内圈多，为了善用这些空间，会将外围的圆分配更多的扇区
	![](https://img.fengqigang.cn//img/20210217212027.png)

![](https://img.fengqigang.cn//img/20210217211521.png)

柱面(cylinder): 所有盘片上面的同一个磁道组合成所谓的柱面

![](https://img.fengqigang.cn//img/20210217212719.png)

### 对于机械硬盘-如何计算它的容量？
![](https://img.fengqigang.cn//img/20210217213715.png)

容量 = 磁道 x 扇区 x 柱面 x Units

![](https://img.fengqigang.cn//img/20210217214042.png)



