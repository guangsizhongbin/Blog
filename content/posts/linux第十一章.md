---
title: "第十一章"
date: 2021-04-18T18:51:33+08:00
lastmod: 2021-04-18
author: "xiaonan"
math:
 enable: true

tags: [linux]
categories: [鸟哥的私房菜]
---

### 正则表达式与万用字符有什么区别?

万用字符 (wildcard) 代表的是 bash 操作接口的一个功能

正则表达式则是一种字串处理的表示方式

### 如何使用 **demesg** 列出核心讯息，再以 **grep** 找出内含 **cpu** 那行，并将捉到的关键字显色表示，且加上行号来表示?

```bash
sudo dmesg | grep -n --color=auto 'cpu'
```

![20210418103848](https://img.fengqigang.cn//img/20210418103848.png)

### 如何使用 **demesg** 列出核心讯息，再以 **grep** 找出内含 **cpu** 那行，并将捉到的关键字显色表示，且加上行号来表示, 同时在关键字所在行的前两行与后三行也一起捉出来显示?

```bash
sudo dmesg | grep -n --color=auto 'cpu'
```

![20210418104030](https://img.fengqigang.cn//img/20210418104030.png)

### 如何捉出 **regular_express.txt** 中有 the 的行, 并提供行号?

```bash
grep -n 'the' regular_express.txt
```

![20210418104410](https://img.fengqigang.cn//img/20210418104410.png)

### 如何捉出 **regular_express** 中没有 the 的行，并提供等行号?

```bash
grep -vn 'the' regular_express.txt
```

![20210418104531](https://img.fengqigang.cn//img/20210418104531.png)


### 如何捉出 **regular_express.txt** 中有 the 的行(包括大小写), 并提供行号?

```bash
grep -in 'the' regular_express.txt
```

![20210418104919](https://img.fengqigang.cn//img/20210418104919.png)

### 如何捉出 **regular_express.txt** 中 test 和 taste 这两个单字?

```bash
grep -n 't[ae]st' regular_express.txt
```

![20210418105141](https://img.fengqigang.cn//img/20210418105141.png)

### 如何捉出 **regular_express.txt** 中 含有 oo 的行，但不想 oo 前有g?

```bash
grep -n '[^g]oo' regular_express.txt
```

![20210418105320](https://img.fengqigang.cn//img/20210418105320.png)

### 如何捉出 **regular_express.txt** 中 含有 oo 的行，但不想 oo 前有是小写字母?

```bash
grep -n '[^[:lower:]oo]' regular_express.txt
```

### 如何捉出 **regular_express.txt** 中 开头不是英文字母小写的行?

```bash
grep -n '^[[:upper:]]' regular_express.txt
```

![20210418110056](https://img.fengqigang.cn//img/20210418110056.png)

### 如何捉出 **regular_express.txt** 中行尾以 . 结束的行?

```bash
grep -n '\.$' regular_express.txt
```

![20210418110628](https://img.fengqigang.cn//img/20210418110628.png)

\ 是用来解除特殊意义的

![20210418110826](https://img.fengqigang.cn//img/20210418110826.png)

**Windows** 的断行字符 `(^M$)`

**Linux** 的断行字符 `$`

### ^ 在字符集合符号([])  与 ([])外有什么不同?

在[]里, [^] 表示反向选择

在[]外, ^[] 表示定位在行首

### 如何找出 regular_express 中的空白行?

'^$'

```bash
grep -n '^$' regular_express.txt
```

### 如何显示 /etc/rsyslog.conf 中不要空白行， 不以#开头的行?

```bash
grep -v '^$' /etc/rsyslog.conf | grep -v '^#'
```

### **grep -n 'goo*g' regular_express.txt** 是什么意思?

* 代表的是 重复0个或多个前面RE字符

goo*g 代表的是 gog, goog, gooog ... 等

![20210418111748](https://img.fengqigang.cn//img/20210418111748.png)

### 如何实现捉出在 regular_express.txt 中以g开头与g结尾的字串,当中的字符可有可无?

```bash
grep -n 'g*g' regular_express.txt
```

这是不可以的

g*g 代表的是g, gg, ggg, gggg

![20210418111932](https://img.fengqigang.cn//img/20210418111932.png)

g.*g 可以实现

. 表示的是一个任意的字符 .

* 可以是0或多个重复前面的字符

```bash
grep -n 'g.*g' regular_express.txt
```

### 如何实现捉出在 regular_express.txt 中以g开头与g结尾的字串,中间有2到5个o的字串?

```bash
grep -n 'go\{2,5\}g' regular_express.txt
```

![20210418182732](https://img.fengqigang.cn//img/20210418182732.png)


### 如何实现捉出在 regular_express.txt 中以g开头与g结尾的字串,中间有2个以上o的字串?

```bash
grep -n 'go\{2,\}g' regular_express.txt
```

![20210418182926](https://img.fengqigang.cn//img/20210418182926.png)

### 如何实现捉出在 regular_express.txt 以 # 开始的那一行，并列出行号?

```bash
grep -n '^#' regular_express.txt
```

![20210418183124](https://img.fengqigang.cn//img/20210418183124.png)


### 如何实现捉出在 regular_express.txt 以 ! 结束的那一行，并列出行号?

```bash
grep -n '!#' regular_express.txt
```

![20210418183230](https://img.fengqigang.cn//img/20210418183230.png)

### 如何实现捉出在 regular_express.txt 以(eve , eae, eee, e e)这样的行，并列出行号?

```bash
grep -n 'e.e' regular_express.txt
```

![20210418183454](https://img.fengqigang.cn//img/20210418183454.png)

### 如何实现捉出在 regular_express.txt 含有单引号有行?

```bash
grep -n  \' regular_express.txt
```

![20210418183546](https://img.fengqigang.cn//img/20210418183546.png)

### 如何实现捉出在 regular_express.txt 有 aay, afy, aly 的行?

```bash
grep -n 'g[afl]y'  regular_express.txt
```

![20210418183914](https://img.fengqigang.cn//img/20210418183914.png)

### 如何实现捉出在 regular_express.txt 有 oog, ood的行, 但不能是 oot 行?

```bash
grep -n 'oo[^t]' regular_express.txt
```

![20210418184132](https://img.fengqigang.cn//img/20210418184132.png)

### 如何实现捉出在 regular_express.txt 中 go 中, 的o 会出现2-3 的行?

```bash
grep -n 'go\{2,3}' regular_express.txt
```

![20210418184437](https://img.fengqigang.cn//img/20210418184437.png)

### 如何以 ls -l 配合 grep 找出  /etc/ 下面文件类型为链接文件属性的文件名?

![20210418184948](https://img.fengqigang.cn//img/20210418184948.png)

链接的标头是 lrwxrwxrwx

```bash
ls -l /etc | grep '^l'
```

![20210418185037](https://img.fengqigang.cn//img/20210418185037.png)





