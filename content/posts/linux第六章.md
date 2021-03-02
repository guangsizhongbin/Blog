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



