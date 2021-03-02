---
title: "Linux第五章"
date: 2021-03-02T21:48:15+08:00
lastmod: 2021-03-02
author: "xiaonan"
math:
 enable: true

tags: [linux]
categories: [鸟哥的私房菜]
---

### ![20210302162007](https://img.fengqigang.cn//img/20210302162007.png) 箭头和方框所指的是什么意思？

1. 第一个箭头是指连接到此文件的数量

2. 第二个箭头指的是文件的容量

3. 方框所指的是文件最后修改的时间

---

### ![20210302162527](https://img.fengqigang.cn//img/20210302162527.png) 如何用ls命令列出全部文件最后修改的确切时间？

`ls -al --full-time`

![20210302162752](https://img.fengqigang.cn//img/20210302162752.png)

---

### ![20210302163122](https://img.fengqigang.cn//img/20210302163122.png)请问testgroup这个群组的成员与其他人(others)是否可以进入本目录？

- test1 是本目录的拥有者，有[rwx]权限，可以对该目录进行任何操作

- testgroup 这个群组[r-x], 即该组的成员可以进入本目录进行工作，但是不能在本目录下进行写入动作。

- other [r--], 由于没有x的权限，因此others的使用者，并不能进入此目录

---

### ![20210302164400](https://img.fengqigang.cn//img/20210302164400.png)系统有个帐号名称为vbird, 这个帐号并没有支持root群组，请问vbird对这个目录有何权限?

vbird 对此目录只有r的权限，但没有x权限，表示vbird没法进入该目录，即便有r权限，也无法执行。

---

### ![20210302165254](https://img.fengqigang.cn//img/20210302165254.png)普通用户dmtsai对这目录/文件的权限为何？

其有r权限，可以查询到文件名，由于没有权限，会有一堆问号

![20210302165615](https://img.fengqigang.cn//img/20210302165615.png)

---

### ![20210302170301](https://img.fengqigang.cn//img/20210302170301.png)为什么很多时候没有/dir1 的r权限，也可以对里面的数据进行操作？

因为， r 代表"这个抽屉里有灯光", 可以看到各个文件在哪里

但当有 x 权限的时候，就知道里面的数据在哪里，不需要有灯光，摸黑也可以找到

只是，没有 r 的话，使用 [tab] 时，无法补齐文件名

---

### 在FHS(filesystem hierarchy standard)规定下，各个文件夹都是放什么的?![20210302171702](https://img.fengqigang.cn//img/20210302171702.png)？[^FHS]
[^FHS]: [Linux Directory Structure (File System Structure) Explained with Examples](https://www.thegeekstuff.com/2010/09/linux-file-system-structure/)

- `/bin` (User Binaries) 与 `/sbin` (System Binaries)

	- `/bin` 与 `/sbin`目录下均是二进制执行文件(binary executables)


- `/etc` (Configuration Files)

	- 所有程序的配置文件都在此

	- 如`passwd`, `shadow`

- `/dev` (Device Files)

	- 所有设备文件都在此


- `/proc` (Process Information)

	- 系统进程的信息都在此

	- 如: `/proc/uptime`

- `/var` (Variable Files)

	- 包含着一些会增加的文件

	- 如: `/var/log`, `/var/lib`, `/var/mail`, `/var/tmp`


- `/tmp` (Temporary Files)

	- 保存着系统和用户生成的临时文件

	- 当系统重启，这里的文件会被删除

- `/usr` (User Programs)

	- 包含着 `/usr/bin`,  `/usr/sbin`, `/usr/lib`, `/usr/local`

- `/home` (Home Directories)

	- 所有用户的家目录在此

	- 如`/home/feng`

- `/boot` (Boot Loader Files)

	- 所有的boot文件在此

	- 如 `efi`, `grub`文件

- `/lib` (System Libraries)
		
	- `bin` 和 `/sbin`所需要的依赖都在此

	- 如: `*.so`

- `/opt` (Optional add-on Apps)
	
	- 第三方软件放置的地方

	- 如: google, netease

- `/mnt` (Mount Directory)

	- 文件挂载的地方

- `/media` (Removable Devices)

	- 可移动媒体设备挂载的地方

- `/srv` (Service Data)

	- 服务数据放置的地方




