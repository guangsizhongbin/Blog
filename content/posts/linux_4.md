---
title: "Linux_4"
date: 2021-02-22T22:24:21+08:00
lastmod: 2021-02-22
author: "xiaonan"
math:
 enable: true

tags: [linux]
categories: [鸟哥的私房菜]
---

### 假设你的主机为虚拟机，里面仅有一颗VirtIO接口的磁盘，请问他在Linux操作系统里面的设备文件名为何？

![](https://img.fengqigang.cn//img/20210222222136.png)

虚拟机使用的是/dev/vd[a-p]来命名的

所以其名为/dev/vda

### 如果你的PC上面有两个SATA磁盘以及一个USB磁盘，而主板上面有六个SATA的插槽，这两个磁盘分别安插在主板上的SATA1, SATA5插槽上，请问这三个磁盘Linux中设备文件名为何？

USB闪存盘与SATA相同，均用/dev/sd[a-p]来命名的

且采用侦测到的顺序来决定设备文件名，并非与实际插槽代号有关

SATA1: /dev/sda

SATA5: /dev/sdb

USB磁盘(开机完成后才被系统捉到): /dev/sdc

