---
title: "Linux_5"
date: 2021-02-25T22:19:48+08:00
lastmod: 2021-02-25
author: "xiaonan"
math:
 enable: true

tags: [linux]
categories: [鸟哥的私房菜]
---


# 主机规划与磁盘分区
## Linux与硬件的搭配
### 各硬件设备在Linux中的文件名
#### 虚拟机中的磁盘名称是什么?
在虚拟机的环境下，为了加速会使用/dev/vd[a-p]这种设备文件名。

#### SATA接口的磁盘名称是什么?
由于SATA/USB/SAS等硬盘接口都是SCSI模块来驱动，因此这些接口的磁盘设备文件都是/dev/sd[a-p]的格式。

## 磁盘分区
### MSDOS(MBR)与GTP磁盘分区表
#### MSDOS的结构是什么样的？

MBR (Master Boot Record, 主要开机记录区)

这个区在磁盘的第一个扇区，其放转置着开机管理程序记录区与分区表

通常为`512 Bytes`

- 主要开机记录区(Master Boot Record, MBR): 可以安装开机管理程序的地方。 `446 Bytes`
- 分区表(partition table): 记录整颗硬盘分区的状态 `64 Bytes`


#### 为什么要分区？

1. 数据安全

重装系统时，各个分区之间不会相互影响


2. 性能考虑

![20210225212740](https://img.fengqigang.cn//img/20210225212740.png)

- P1: /dev/sda1
- P2: /dev/sda2
- P3: /dev/sda3
- P4: /dev/sda4


#### 分区表只记录四组数据，则分出多于四个分区是如何实现的？

![20210225213049](https://img.fengqigang.cn//img/20210225213049.png)

P1 为主要分区(Primary)

p2 为延伸分区(Extended)

p2分出来的L1, L2, L3, L4, L5为逻辑分区(logical partition)

设备文件名分别为:

- P1: /dev/sda1
- P2: /dev/sda2
- L1: /dev/sda5
- L2: /dev/sda6
- L3: /dev/sda7
- L4: /dev/sda8
- L5: /dev/sda9


`/dev/sda3与/dev/sda4`是保留给Primary或Extended用的，逻辑分区的设备名称号码由5号开始

#### ![20210225213713](https://img.fengqigang.cn//img/20210225213713.png)?

1. 当D与E盘均属于延伸分区内的逻辑分区，将两个分区删除，然后再重新创建一个新的分区，能够在不影响其他分区的情况下，将两个分区的容量整合成为一个。

2. 当D与E分属于主分区与逻辑分区时，两者不能够整合在一起，除非将延伸分区破坏掉后再重新分区。但如此一来会影响到所有的逻辑分区。


#### ![20210225214253](https://img.fengqigang.cn//img/20210225214253.png)?

1. 因为P(Primary) + E(Extended)最多只能有四个，若有4个P了，即便还有剩余容量，因为无法再继续分区，所以容量就被浪费掉了

2. 想要将所有的四笔记录都花光，则P+P+P+E比较好

#### ![20210225214729](https://img.fengqigang.cn//img/20210225214729.png) 

因为P(Primary) + E(extended)最多为4个

1. P+P+P+E的环境
![20210225215235](https://img.fengqigang.cn//img/20210225215235.png)
2. P+E的环境
![20210225215248](https://img.fengqigang.cn//img/20210225215248.png)

#### 为什么会出现GPT?

1. 操作系统无法抓取到2.2T以上的磁盘容量

2. MBR仅有一个区块，若被破坏后，经常无法或很难援救

3. MBR内的存放开机管理程序的区块仅446Bytes, 无法容纳较多的程序码

#### GPT的结构是什么样的？

GPT: GUID partition table

![20210225215857](https://img.fengqigang.cn//img/20210225215857.png)

- LBA0 (MBR相容区块)
	- `446 Bytes` 第一阶段开机管理程序
	- 特殊标志分区,用来表示此磁盘为GPT格式

- LBA1 (GPT表头纪录)
	- 分区表本身的位置与大小
	- 备份用的GPT分区(最后34个LBA区块)放置位置
	- 分区表的检验机制码(CRC32)
	
- LBA2-33 (实际纪录分区信息处)
	- 每个LBA可以记录4笔分区记录， 即32*4笔记录
	- 每个LBA有512 Bytes, 则每笔记录用于128 Bytes的空间
	- GPT在每笔记录中分别提供了 64 bits 来记载开始/结束的磁区号码
	- 对于GPT分区表对于单一分区来说，它的最大容量为:$2^{64} *512bytes = 2^{63} * 1Kbytes = 2^{33}*TB = 8 ZB$

### 开机流程中的BIOS与开机检测程序

### 主机的服务规划与硬件的关系


