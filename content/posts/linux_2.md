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


