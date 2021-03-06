---
title: "Linux第九章"
date: 2021-03-21T10:30:12+08:00
lastmod: 2021-03-21
author: "xiaonan"
math:
 enable: true

tags: [linux]
categories: [鸟哥的私房菜]
---
### 什么是纯文本文件?

文件记录就是0与1, 面通过编码系统将这些0与1转成如我们认识的文字

### 在 **vim** 中,  n + <space> 代表什么操作?

表示光标会向 **右** 移动 **n** 个字符

### 在 **vim** 中, 如何移动到这一列的最后面字符处?

**$**

### 在 **vim** 中, 如何将光标移动到这个屏幕中央那一列的第一个字符?

M

### 在 **vim** 中, 如何移动到第n行?

nG

### 在 **vim** 中, 光标如何向下移动n行?

n <Enter>

### 在 **vim** 中, 如何在第 **n1** 与 **n2** 列之间寻找 **word1** ， 并将该字串取代为 **word2**?

```bash
:n1, n2s/word1/word2/g
```

### 在 **vim** 中，如何在第一行到最后一行寻找 **word1** 字串，并将该字串取为 **word2**, 且在取代前显示提示字符给使用者确认?

```bash
:1, $1/word1/word2/gc
```

### 在 **vim** 中，如何在第一行到最后一行寻找 **word1** 字串，并将该字串取为 **word2**?


```bash
:1, $1/word1/word2/g
```

### 在 **vim** 中， 如何向后删除n个字符?

nx

### 在 **vim** 中， 如何向前删除n个字符?

nX

### 在 **vim** 中， 如何删除光标所在行到第一行的所有数据?

d1G

### 在 **vim** 中， 如何删除光标所在行到最后一行的所有数据?

dG

### 在 **vim** 中， 如何删除光标所在处，到该列的最后一个字符?

**d$**

### 在 **vim** 中， 如何删除光标所在处，到该列的最前面的一个字符?

**d0**

### 在 **vim** 中， 如何复制光标所在行到第一行的所有数据?

y1G

### 在 **vim** 中， 如何复制光标所在行到最后一行的所有数据?

yG

### 在 **vim** 中, 如何复制光标所在的那个字符到该列行首的所有数据?

y0

### 在 **vim** 中, 如何复制光标所在的那个字符到该列行尾的所有数据?

**y$**

### 在 **vim** 中, 如何使光标所在行与下一行的数据结合成同一行?

J

### 在 **vim** 中， 如何复原前一个动作?

u

### 在 **vim** 中， 如何重做上一个动作?

[Ctrl] + r

### 在 **vim** 中，如何将已复制的数据在光标下一列贴上?

p

### 在 **vim** 中，如何将已复制的数据在光标上一列贴上?

P

### 在 **vim** 中，如何重复前一个动作?

.

### 在 **vim** 中， 如何在当前光标所在的下一个字符处开始插入?

a

### 在 **vim** 中， 如何在当前光标所在的上一列插入新的一列?

O

### 在 **vim** 中， 如何取代光标所在的那一个字符一次?

r

### 在 **vim** 中， 如何取代光标所在的文字，直到按下 **ESC** 为止?

R

### 在 **vim** 中， 如何实现若文件没有更动，则不储存离开，若文件已经被更动过，则储存后离开?

ZZ

### 在 **vim** 中, 如何实现在编辑的数据中，读入另一个文件的数据，将 **fielname** 这个文件内容加到光标所在的后面？

:r [filename]

### 在 **vim** 中， 如何实现将 **n1** 到 **n2** 的内容储存成 **filename** 这个文件中?

:n1, n2 w [filename]

### 在 **vim** 中， 如何暂时离开 **vim**, 执行 **bash** 中的命令?

:! command

### 在 **vim** 中， 如何设置显示行号?

:set nu

### 在 **vim** 中， 如何进行区块选择（用长方形的方式选择数据）?

[Ctrl] + V

### 如何列出目前这个 **vim** 打开的所有文件?

`:files`


### 在 **vim** 中， 若同时打开多个文件，如何编辑下一个文件？

`:n`

### 在 **vim** 中， 若同时打开多个文件，如何编辑上一个文件？

`:N`

### 在 **vim** 中， 如何以当前目录内的"文件名"作为关键字，予以补齐?

**[ctrl] + x --> [Ctrl] + f**

**file** 

CTRL-x_CTRL-F

### 在 **vim** 中， 如何以正在编辑的这个"文件的内容文字"作为关键字，予以补齐?

**[ctrl] + x --> [Ctrl] + n**

**Keywords in the current file** 

CTRL-x_CTRL-n

### 在 **vim** 中， 如何以扩展名作为语法补充，以 **vim** 内置的关键字，予以补齐?

**[ctrl] + x -> [ctrl] + O**

**omni completion**

CTRL-x_CTRL-O

### **~/.viminfo** 保存的是什么?

它是记录动作的文件.

![20210328093854](https://img.fengqigang.cn//img/20210328093854.png)

### 如何查看到文件中的断行字符?

**cat -A**

![20210328094903](https://img.fengqigang.cn//img/20210328094903.png)

### **window** 与 **linux** 中的断行字符是否相同?

不同


![20210328094903](https://img.fengqigang.cn//img/20210328094903.png)

![20210328095202](https://img.fengqigang.cn//img/20210328095202.png)

###  如何将 **/etc/man_db.conf** 重新复制到 **/tmp/vitest** 下面，并将其修改成为 **dos** 断行?

```bash
cd /tmp/vitest

cp -a /etc/man_db.conf /tmp/vitest/

unix2dos -k man_db.conf
```

![20210328100613](https://img.fengqigang.cn//img/20210328100613.png)

**dos2unix**

DOS/Mac to unix and vice versa text file format converter

**-k**

Keep the data stamp of output file same as input file

### 如何将 **man_db.conf** 转成 **Linux** 断行字符, 并保留旧文件，新文件放于 **man_db.conf.linux**

```bash
dos2unix -k -n man_db.conf man_db.conf.linux
```

![20210328100843](https://img.fengqigang.cn//img/20210328100843.png)

**-k**

Keep the data stamp of output file same as input file

**-n, --newfile INFILE OUTFILE ...**

New file mode. Convert file INFILE and write output to file OUTFILE.	

### 如何查看一个文件是 **win** 下创建的文件还是 **linux** 下创建的文件？

```bash
file man_db.conf*
```

![20210328100934](https://img.fengqigang.cn//img/20210328100934.png)

### 如何将 **vi.big5** 这个文件转成 **vi.utf8**?

iconv -f BIG5 -t utf8 vi.big5 > vi.utf8

![20210328101405](https://img.fengqigang.cn//img/20210328101405.png)

**iconv**

convert text from one character encoding to another

**-f from-encoding, --from-code=from0encoding**

Use from-encoding for input characters

**-t to-encoding, --to-code=to-encoding**

Use to-encoding for output characters.




