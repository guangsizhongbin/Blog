---
title: "Linux第六章"
date: 2021-03-02T21:49:05+08:00
lastmod: 2021-03-02
author: "xiaonan"
math:
 enable: true

tags: [linux]
categories: [鸟哥的私房菜]
---

### ![20210302190450](https://img.fengqigang.cn//img/20210302190450.png)如何回到之前的目录？

`cd -`

---

### ![20210302191131](https://img.fengqigang.cn//img/20210302191131.png)如何显示其正确的完整路径，而不是其链接的数据显示?

`pwd -P`

![20210302191248](https://img.fengqigang.cn//img/20210302191248.png)

---

### 如何创建一次创建 `test1/test2/test3/test4` 这样的目录， `/test1~4`均未创建?

`mkdir -p test1/test2/test3/test4`

`-p --parents:`

no error if existing, make parent directories as needed.

![20210302191718](https://img.fengqigang.cn//img/20210302191718.png)


--- 

### 如何创建一个权限为`rwx--x--x`的目录`test2`?

`mkdir -m 711 test2`

`-m --mode=MODE:`

set file mode (as in chomd), not a=rwx - umask

![20210302192336](https://img.fengqigang.cn//img/20210302192336.png)

---

### 如何使root在任何目录均可执行`/root`下面的ls?

`PATH = "${PATH}:/root"`

---

### 如何复制 `/var/log/wtmp`文件到 `~/wtmp_2`, 并且它的文件权限一模一样?

cp -a

`-a, --archive`


![20210302194445](https://img.fengqigang.cn//img/20210302194445.png)

---

### 如何创建`bashrc`的实体链接(hard link)和符号链接(symbolic link)?

![20210302195555](https://img.fengqigang.cn//img/20210302195555.png)


---

### 如何当 `~/.bashrc` 比 `/tmp/bashrc` 新时则复制?

cp -u ~/.bashrc /tmp/bashrc

`-u, --update`
	
	copy only when the SOURCE file is newer than the destination file or when the destination file is missing

---

### 若`bashrc_slink`是软链接文件，则![20210302202250](https://img.fengqigang.cn//img/20210302202250.png)复制的是什么？

没有加任何选项时，cp复制的是原始文件，而非链接文件的属性

若加`-d`选项，则复制的是链接文件的属性


`-d`
	
	same as --no-dereference --preserve=links

---

### 能否使用feng的身份，完整的复制`/var/log/wtmp`文件到`/tmp`下面？

![20210303101458](https://img.fengqigang.cn//img/20210303101458.png)

因为feng身份并不能随意修改文件的拥有者与群组，因此虽然能够复制wtmp的相关权限与时间等属性，但是与拥有者、群组相关的，feng无法身份无法进行操作。

---

### 如何获取 `/etc/sysconfig/network` 中最后的文件名？

`basename /etc/sysconfig/network`

![20210303102017](https://img.fengqigang.cn//img/20210303102017.png)

---

### 如何获取 `/etc/sysconfig/network` 的目录名？

`dirname /etc/sysconfig/network`

![20210303102123](https://img.fengqigang.cn//img/20210303102123.png)

---

### 如何使 `cat /etc/issue` 能够显示行号？

`cat -n /etc/issue`

`-n, --number`
	
	number all output lines

![20210303102338](https://img.fengqigang.cn//img/20210303102338.png)


--- 

### 如果只想列出 `/etc/man_db.conf` 前20行， 该如何操作？

`head - n 20 /etc/man_db.conf`

![20210303102849](https://img.fengqigang.cn//img/20210303102849.png)

---

### 如何只想列出 `/etc/man_db.conf` 最后20行，该如何操作？

`tail -n 20 /etc/man_db.conf`

![20210303103032](https://img.fengqigang.cn//img/20210303103032.png)

-- 

### 不知道`/etc/man_db.conf`有几行，但想列出120行后的数据，该如何操作？

`tail -n +120 /etc/man_db.conf`

![20210303103247](https://img.fengqigang.cn//img/20210303103247.png)

---

### 如何想显示 `/etc/man_db.conf`的第11到第20行，该如何操作？

`head -n 20 /etc/man_db.conf | tail -n 10`

![20210303103500](https://img.fengqigang.cn//img/20210303103500.png)

---


### 如何想显示 `/etc/man_db.conf`的第11到第20行，且行号存在， 该如何操作？

`cat -n /etc/man_db.conf | head -n 20 | tail -n 10`

![20210303103656](https://img.fengqigang.cn//img/20210303103656.png)

--- 

### 如何将`/usr/bin/passwd`的内容用ASCII方式展现？

`od -t c /usr/bin/passwd`

---

### 如何将`/etc/issue`这个文件内容以8进位列出储存值与ASCII的对照表?

`od -t oCc /etc/issue`

-t: `-t, --format=Type`
	
	Select output format or formats

C: `SIZE may also be C for sizeof(char)`

c: `printable character or backslash escape`

o: `octal, SIZE bytes per integer`

![20210303104914](https://img.fengqigang.cn//img/20210303104914.png)

---

### 如何立即找到password这几个字的ASCII对照， 该如何通过od来判断？

echo password | od -t oCc echo

![20210303105534](https://img.fengqigang.cn//img/20210303105534.png)

---

### 当复制一个文件时，复制所有的属性，ctime这个属性可以复制吗？

不可以， `ctime` 是记录这个文件最近的状态(status)被改变的时间

![20210303110734](https://img.fengqigang.cn//img/20210303110734.png)

`mtime`: 文件的"内容数据"变更时，就会更新这个时间

`ctime`: 文件的状态更改时，就会更新这个时间

`atime`: 当文件被取用时，会更新这个时间

---

### 若你的系统有个一般身份使用者 feng, 他的群组属于 feng, 他的主文件夹在 /home/dmtsai, 你是root, 你想将你的~/.bashrc复制给他，可以怎么作？

cp ~/.bashrc ~feng/bashrc

chown feng:feng ~feng/bashrc

---

### 我想在 /tmp 下面创建一个目录，这个目录名称为 chapter6_1, 并且这个目录拥有者为 feng, 群组为feng, 此外，任何人都可以进入该目录浏览文件，不过除了feng之外，其他人都不能修改这目录下的文件

整个目录权限应为 `drwxr-xr-x`

mkdir /tmp/chapter6_1

chown -R feng:feng /tmp/chapter6_1

chmod -R 755 /tmp/chapter6_1

