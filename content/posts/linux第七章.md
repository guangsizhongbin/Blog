---
title: "Linux第七章"
date: 2021-03-06T12:32:45+08:00
lastmod: 2021-03-06
author: "xiaonan"
math:
 enable: true

tags: [linux]
categories: [鸟哥的私房菜]
---

### 为什么硬盘在分区后需要进行格式化呢?

因为每个操作系统所设置的文件属性/权限并不相同，为了存放这些文件所需的数据，因此就需要将分区进行格式化, 以成为操作系统能够利用的文件系统格式。

### 在ext2中, superblock, inode和block是什么样的关系?

**superblock** : 记录此 **filesystem**的整体信息，包括inode/block的总量、使用量、剩余量，以及文件系统的格式与相关信息。

**inode**: 记录文件的属性，一个文件占用一个inode, 同时记录此文件的数据所在的block号码。

**block**: 实际记录文件的内容，若文件太大时，会占用多个block

![20210306104037](https://img.fengqigang.cn//img/20210306104037.png)

### 为什么在window系统下常听到需要磁盘整理？

如U盘，其文件格式是FAT, 这种文件格式没有inode存在，因此FAT没法将这个文件的所有block在一开始就读取出来

**其采取的方法是这样的**

![20210306104251](https://img.fengqigang.cn//img/20210306104251.png)

当数据过于离散的时候，读取一个文件有可能要转好几圈。

### 若Ext2文件系统使用4K block, 而该文件系统中有10000个小文件，每个文件大小均为50Bytes, 请问此时磁盘会浪费多少容量?

在Ext2文件系统中一个block仅能容纳一个文件，

则一个文件将浪费4096 - 50 = 4046 Bytes.

4046 * 10000 / 1024 / 1024 = 38. 58MB

### 如何找出目前系统有被格式化的设备?

**blkid**

**\*\* locate/print block device attributes ****

![20210306095400](https://img.fengqigang.cn//img/20210306095400.png)

### 每个inode大小均固定为128bytes, 而inode记录一个block号码要花掉4byte, 假设一个文件有400MB, 且每个block为4KB，那么至少也要10万条block号码的记录，inode哪有这么多的可以记录的信息？它采用了什么样的方法解决这个问题?

系统将indoe 记录的block号码的区域定义为12个直接，一个间接，一个双间接，与一个三间接记录区

![20210306105450](https://img.fengqigang.cn//img/20210306105450.png)

则若一个block为1KB,

12个直接: 12 x 1KB = 12KB

1个间接: 256 x 1KB = 256KB

**每条block号码的记录会花去 4bytes, 因此1KB 的大小能记录256条记录**

1个双间接: 256 x 256 x 1KB = $256^2$ KB

1个三间接: 256 x 256 x 256 x 1KB = $256^3$ KB

即: 当文件系统将block格式化为1K大小时，能够容纳最大文件为16GB

![20210306110539](https://img.fengqigang.cn//img/20210306110539.png)

### 若在Linux下的ext2文件系统新建一个目录，ext2会做什么？

**ext2** 至少会分配一个 **inode** 与至少一块 **block** 给该目录

**inode** 记录该目录的相关权限与属性, 并记录分配到的那块block号码

**block** 则是记录在这个目录下的文件名与该文件名占用的 **inode** 号码数据

### 如何查看root目录内的文件所占用的inode号码?

**ls -li**

-i, --inode

print the index number of each file

![20210306111643](https://img.fengqigang.cn//img/20210306111643.png)

### 为什么这些文件夹的大小都是1024的倍数?![20210306111904](https://img.fengqigang.cn//img/20210306111904.png)

因为 **/dev/sda2** 采用的 **Block size** 为 **4096**

![20210306112234](https://img.fengqigang.cn//img/20210306112234.png)

### 为什么 **/proc** 文件夹的大小为0? ![20210306112557](https://img.fengqigang.cn//img/20210306112557.png)

因为这个目录是一个虚拟文件系统(virtual filestem). 它放置的数据都是在内存当中。

因为这个目录下的数据都是在内存当中，所以本身不占任何硬盘空间。

### 若在ext2下新建一个100KB的文件，block为4KB, ext2会怎么做?

在linux下的ext2新建一个文件时，ext2分分配一个inode与相对于该文件大小的block数量给该文件。

当文件为100KB时，linux会分配一个 **inode**, 与25个 **block**来记录数据

但inode仅有12个直接指向 **block记录** ，因此还要多一个block间接指向另外的13个 **block记录**

![20210306114906](https://img.fengqigang.cn//img/20210306114906.png)

### ext2是如何读取 **/etc/passwd**这个文件的?![20210306115242](https://img.fengqigang.cn//img/20210306115242.png)

1.  \*\*/\*\* 的 inode: 通过挂载点的信息找到inode号码为2的根目录inode, 且 **inode** 规范的权限让我们可以读该block的内容(有r与x)
    
2.  \*\*/\*\* 的 block: 通过上个步骤取得block的号码，并找到该内容有 **/etc** inode号码(5767169)
    
3.  \*\*etc/\*\* 的 inode: 读取5767169号 inode 得知feng具有r与x权限，因此可以读取 **etc/** 的block内容
    
4.  \*\*etc/\*\* 的 block: 经过上个步骤取得block号码，并找到有 **passwd** 文件的 **inode** 号码 (5775935)
    
5.  **passwd** 的inode: 读取 5775935 号inode得知feng具有r的权限，因此可以读取**passwd**的内容
    
6.  **passwd** 的block: 最后将该block内容的数据读出来

### 如何需要新建一个文件或目录时，Ext2是如何处理的呢?

1. 先确定用户对欲添加文件的目录是否具有w与x的权限，若有的话才能添加

2. 根据 **inode bitmap** 找到没有使用的 **inode** 号码， 并将新文件的权限/属性写入

3. 根据 **block bit map** 找到没有使用的 **block** 号码， 并将实际的数据写入 **block** 中， 且更新 **inode** 的 **block** 指向数据

4. 将刚才写入的 **inode** 与 **block** 数据同步更新 **inode bitmap** 与 **block bitmap**, 并更新**superblock**的内容

### 若在新建一个文件的时候，仅写入 **inode table** 及 **data block** ， 但因突然停电 **inode bitmap** 与 **block bitmap**, **superblock**都没有更新，此时linux是如何解决这个问题的?

**文件系统中会规划出一个块，该块专门记录写入或修订文件时的步骤**

1. 预备: 当系统要写入一个文件时，会先在日志记录块中记录某个文件准备要写入的信息

2. 实际写入: 开始写入文件的权限与数据；开始更新meta data的数据

3. 结束: 完成数据与 meta data 的更新后，在日志记录块当中完成文件的记录



![20210307101155](https://img.fengqigang.cn//img/20210307101155.png)

### **/ /. /..** 是什么关系?

![20210307102029](https://img.fengqigang.cn//img/20210307102029.png)

**/ /. /..** 三个文件所对应的 **inode** 是2, 它们都是相同的，所以这几个文件是相同的

### 如何将系统内所有的文件系统列出来?

**df**

![20210307102439](https://img.fengqigang.cn//img/20210307102439.png)

### 如何将系统内所有的文件系统更出来同时容量结果以易读的容量格式显示出来?

**df -h**

**-h, --human-readable**

print sizes in powers of 1024


![20210307102604](https://img.fengqigang.cn//img/20210307102604.png)

### 如何将系统内所有特殊文件格式入名称及名称都列出来, 如 **/proc** 挂载点的文件?

**df -aT**

**-a, --all**

include pseudo, duplicate, inaccessible file systems

**-T, --print-type**

print file system type

![20210307103044](https://img.fengqigang.cn//img/20210307103044.png)

### 如何将 **/etc** 下面的可用的磁盘容量以容量以易读的容量格式显示?

**df -h /etc**

![20210307103234](https://img.fengqigang.cn//img/20210307103234.png)

### 如何将目前各个分区当中可用的 **inode** 数量列出?

**df -ih**

![20210307103412](https://img.fengqigang.cn//img/20210307103412.png)

### 如何列出目录下所有目录的容量，包括自己?

**du**

![20210307103915](https://img.fengqigang.cn//img/20210307103915.png)

### 如何列出目录下所有文件的容量?

**du -a**

**-a, --all**

write counts for all files, not just directories

![20210307104030](https://img.fengqigang.cn//img/20210307104030.png)

### 如何检查根目录下面每个目录所占用的容量?

**sudo du -sm /***

**-s, --summarize**

display only a total for each argument

**-m**

like --block-size=1M


### hard link的原理是什么样的?

![20210307104833](https://img.fengqigang.cn//img/20210307104833.png)


