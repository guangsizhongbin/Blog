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

### 如何将 **/etc/passwd** 的内容列出并且打印出行号，同时，将第2~5行删除?

```bash
nl /etc/passwd | sed '2,5d'
```

![20210421144435](https://img.fengqigang.cn//img/20210421144435.png)

### 如何将 **/etc/passwd** 的内容列出并且打印出行号，同时删除第2行?

```bash
nl /etc/passwd | sed '2d'
```
![20210421144740](https://img.fengqigang.cn//img/20210421144740.png)

### 如何将 **/etc/passwd** 的内容列出并且打印出行号，同时删除第3行到最后一行?

```bash
nl /etc/passwd | sed '3,$d'
```

![20210421145028](https://img.fengqigang.cn//img/20210421145028.png)

### 如何将 **/etc/passwd** 的内容列出并且打印出行号，并在第二行后加上 drink tea 字样?

```bash
nl /etc/passwd | sed '2a drink tea'
```
a \ 

text Append text, which has each embedded newline preceded by a backslash.

![20210421145219](https://img.fengqigang.cn//img/20210421145219.png)

### 如何将 **/etc/passwd** 的内容列出并且打印出行号，并在第二行前加上 drink tea 字样?

```bash
nl /etc/passwd | sed '2i drink tea'
```

i \ 

text Insert text, which has each embedded newline preceded by a blackslash

![20210421145344](https://img.fengqigang.cn//img/20210421145344.png)

### 如何将 **/etc/passwd** 的内容列出并且打印出行号，并在第二行后加上 Drink tea or ... 换行 drink beer? ?

```bash
nl /etc/passwd | sed '2a Drink tea or ... \
> drink beer?'
```
a \ 

text Append text, which has each embedded newline preceded by a backslash.


![20210421145756](https://img.fengqigang.cn//img/20210421145756.png)

### 如何将 2-5 行的内容取代为 "No 2-5 number"?

```bash
nl /etc/passwd | sed '2,5c No 2-5 number'
```
c \ 

text Replace the selected lines with text, which has each embedded newline preceded by a backslash.

### 如何用 sed 仅列出 5,7 行的内容?

```bash
nl /etc/passwd | sed -n '5,7p'
```

n N 

Read/append the next line of input into the pattern space.

### 输出 **/etc/man_db.conf**， 抓取有 MAN 的行， 去掉有 # 的行， 空白行?

1. 查找有 MAN 的行

```bash
cat /etc/man_db.conf | grep 'MAN'
```

2. 去掉有 # 的行

```bash
cat /etc/man_db.conf | grep 'MAN' | sed 's/#.*$//g'
```
![20210421151806](https://img.fengqigang.cn//img/20210421151806.png)

3. 删除空白行

```bash
cat /etc/man_db.conf | grep 'MAN' | sed 's/#.*$//g' | sed '/^$/d'
```
![20210421152028](https://img.fengqigang.cn//img/20210421152028.png)

### 如何用 sed 将 **regular_express.txt** 内第一行结尾若为 . 则换成 **!** ?

```bash
sed -i 's/\.$/\!g' regular_express.txt
```

![20210421152336](https://img.fengqigang.cn//img/20210421152336.png)

### 如何用 sed 直接在 **regular_express.txt** 最后一行 "# This is a test"?

```bash
sed -i '$a # This is a test' regular_express.txt
```

![20210421152625](https://img.fengqigang.cn//img/20210421152625.png)

### 如何用 **last** 登录者的数据取出来, 并取出前5行，列出第1列和第3列的数据，中间以tab格开?

```bash
last -n 5 | awk '{print $1 "\t" $3}'
```
![20210422222134](https://img.fengqigang.cn//img/20210422222134.png)

### 如何用 **last** 显示出登录者的前5行，抽取取用户名，显示当前处理行数, 该行有多少字段?

```bash
last -n 5 | awk '{print $1 "\t lines " NR " \t columns: " NF}'
```

**NF**

The number of fields in the current record

**NR**

The ordinal number of the current record from the start of input.

![20210422223540](https://img.fengqigang.cn//img/20210422223540.png)

### 如何从/etc/passwd(以冒号来作为字段的分隔), 文件中第一字段为账号, 第三字段则是 UID, 找出第三栏小于10以下的数据，并且仅列出账号与第三栏?

```bash
cat /etc/passwd | awk '{FS=":"} $3 < 10 {print $1 " \t " $3}'
```

![20210422224722](https://img.fengqigang.cn//img/20210422224722.png)


### ![20210422224722](https://img.fengqigang.cn//img/20210422224722.png)
为什么仅能在第二行才开始生效?

因为在读入第一行的时候，那些变量 $1, $2, 默认还是以空白键为分隔的，所以虽然定义了 FS=":". 仅能在第二行后才开始生效

### ![20210422224722](https://img.fengqigang.cn//img/20210422224722.png)
如何在第一行也可以生效?

预先设置 awk 的变量， 利用 BEGIN 这个关键字

```bash
cat /etc/passwd | awk 'BEGIN {FS=':'} $3 < 10 {print $1 " \t " $3}'
```

![20210422225229](https://img.fengqigang.cn//img/20210422225229.png)

### ![20210424113513](https://img.fengqigang.cn//img/20210424113513.png) 这两个代表什么意思?

4d3

左边第4行被删除 (d) 掉了, 基准是右边的第三行

6c5

左边文件的第六行被取代 (c) 成右边文件的第五行

![20210424115224](https://img.fengqigang.cn//img/20210424115224.png)

### 如何对比 **github/Blog** 与 **github/Momo** 两个目录之间的差异?

```bash
diff github/Blog github/Momo
```

![20210424115422](https://img.fengqigang.cn//img/20210424115422.png)

### diff 与 cmp 有什么区别?

diff 主要是以 "行" 为单位比对

cmp 则是以 "字节" 为单位比对

### 如何在字节上对比， **passwd.old**, **passwd.new**?

```bash
cmp passwd.old passwd.new
```

![20210424115722](https://img.fengqigang.cn//img/20210424115722.png)


