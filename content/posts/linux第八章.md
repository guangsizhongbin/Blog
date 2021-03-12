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


### 如何将 **/root/etc.tar.bz2** 解压到 **/tmp** 下?

**tar -jxv -f /root/etc.tar.bz2 -C /tmp**

**-C, --directory=DIR**

Change to DIR before performing any operations. This option is order0sensitive, i.e. it affects all options that follow.


**-j, --bzip2**

Filter the archive through bzip2

**-v, --verbose**

Verbosely list files processed. Each instance of this option on the command line increases the verbosity level by one. The maximum verbosity level is 3.

### 如何将 **/root/etc.tar.bz2** 中的 **etc/shadow** 解压出来?

1. 找一找看有没有 **shadow**

**tar -jtv -f /root/etc.tar.bz2 | grep 'shadow'**


**-j, --bzip2**

Filter the archive through bzip2

**-t, --list**

List the contents of an archive. Arguments are optional. When given, they specify the names of the members to list.

**-v, --verbose**

Verbosely list files processed. Each instance of this option on the command line increases the verbosity level by one. The maximum verbosity level is 3.

2. 解压 **etc/shadow**

**tar -jxv -f /root/etc.tar.bz2 etc/shadow**

### 若想用 **tar** 打包 **/etc /root** 但不想打包 **/root/etc*** 开头的文件，该如何做?

**--exclude=**

tar -jcv -f /root/system.tar.bz2 --exclude=/root/etc* \
--exclude=/root/system.tar.bz2 /etc /root

不包括 **/root/etc**, 同时不能包括自己

### 如何用 **tar** 备份 **/etc/passwd** 中比 **/etc/passwd** 还要新的文件?

1. 找出比 **/etc/passwd** 还要新的文件

**find /etc -newer /etc/passwd**

2. 查看 **/etc/passwd** 的 **mtime**

![20210312101216](https://img.fengqigang.cn//img/20210312101216.png)

3. 打包

tar -jcv -f /root/etc.newer.then.passwd.tar.bz2 \
--newer-mtime="2021/03/01" /etc/*

4. 显示出文件

tar -jtv -f /root/etc.newer.then.passwd.tar.bz2 | grep -v "/$"

调出非 / 的文件名

### 如何将 **/home,  /root, /etc** 备份到磁带机 **/dev/st0** 上?

tar -cv -f /dev/st0 /home /root /etc

### 如何用 **tar** 一边将 **/etc** 整个目录打包一边在 **/tmp** 解开?

tar -cvf - /etc | tar -xvf -

**-**

表示被打包的文件

### 如何用 **tar** 对系统备份?

- /etc/ (配置文件)

- /home/ (使用者的主文件夹)

- /var/spool/mail/ (系统中，所有账号的邮件信箱)

- /var/spool/cron/ (所有账号的工作排成配置文件)

- /root (系统管理员的主文件夹)

1. 设置备份数据的目录与权限

mkdir /backups

chmod 700 /backups

ls -d /backups

![20210312102701](https://img.fengqigang.cn//img/20210312102701.png)

2. 备份

tar -jcv -f /bakups/backup-system-20210312.tar.bz2 \
/etc /home /var/spool/mail /var/spool/cron /root



