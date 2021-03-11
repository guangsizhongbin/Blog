---
title: "Linux第八章"
date: 2021-03-11T09:56:33+08:00
lastmod: 2021-03-11
author: "xiaonan"
math:
 enable: true

tags: [linux]
categories: [鸟哥的私房菜]
---

### 什么是压缩的原理是什么?

**压缩** : 

如果数据为"111..."共用100个, 压缩技术会记录为"100个1"而不是真的有100个1的位存在

### 如何用 **tar** 备份 **/etc** (tar.gz)?

1. 切换成 **root** 用户

2. **time tar -zpcv -f /root/etc.tar.gz /etc**

**-z, --gzip, --gunzip, --ungzip**

Filter the archive through gzip

**-p, --preserve-permissions, --same-permissions**

extract information about file permissions(default for superuser)

**-c, --create**

Cteate a new archive. Arguments supply the names of the files to be archived. Directories are archived recursively, unless the --no-recursion option is given.

**-v, --verbose**

Verbosely list files processed. Each instance of this option on the command line increases the verbosity level by one. The maximum verbosity level is 3.

**-f, --file=ARCHIVE**

Use archive file or device ARCHIVE

### 用 **tar** 备份时， **.tar.gz**, **tar.bz2**, **tar.xz** 分别要对应什么参数?

**.tar.gz** 

time tar -zpcv -f /root/etc.tar.gz /etc

**-z, --gzip, --gunzip, --unzip**

Filter the archive through gzip.

![20210311090026](https://img.fengqigang.cn//img/20210311090026.png)

**tar.bz2**

time tar -jpcv -f /root/etc.tar.bz2 /etc

**-j, --bzip2**

Filter the archive through bzip2

![20210311090102](https://img.fengqigang.cn//img/20210311090102.png)

**tar.xz**

time tar -Jpcv -f /root/etc.tar.xz /etc

**-J, --xz**

Filter the archive through xz

![20210311090143](https://img.fengqigang.cn//img/20210311090143.png)

![20210311090253](https://img.fengqigang.cn//img/20210311090253.png)


### 如何查看 **/root/etc.tar.bz2** 内的文件?

**tar -jtv -f /root/etc.tar.bz2**

**-t, --list**

List the contents of an archive. Arguments are optional. When given, they specify the names of the members to list.

![20210311091945](https://img.fengqigang.cn//img/20210311091945.png)

### 为什么查看 **/root/etc.tar.bz2** 里面的文件，都没有根目录?![20210311092259](https://img.fengqigang.cn//img/20210311092259.png) 

如果拿掉根目录，假设备份数据在 **/tmp** 解开，那么解压缩的文件就会变成 **/tmp/etc/**

如果没有拿掉根目录,解压缩的文件名就会是绝对路径，数据一定会放置到 **/etc** 中去

### **tar -jcvf filename** 和 **tar -jvfc filename** 是一样的吗?

不一样

-jvfc 会导致产生的文件名变成 **c**

最好将 **-f filename** 与其他选项项独立出来







