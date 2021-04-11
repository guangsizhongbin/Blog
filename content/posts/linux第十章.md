---
title: "Linux第十章"
date: 2021-04-04T11:22:35+08:00
lastmod: 2021-04-04
author: "xiaonan"
math:
 enable: true

tags: [linux]
categories: [鸟哥的私房菜]
---

### 什么是壳程序?

能够操作 **应用程序的接口** 都能够称为壳程序

**狭义**:

命令行方面的软件

**广义**:

包括图形接口的软件

### 在 **linux** 把运行过后的指令保存在哪里?

**~/.bash_history**

**~/.bash_history** 记录的是前一次登录以前执行过的指令

而至于这一次登录所执行的指令都被 **暂存在内存中** ,  当成功的登出系统后，该指令记忆才会记录到 **.vash_history** 当中

### 如何查看 **cd** 是否是 **bash** 的内置命令?

**type cd**

![20210404094640](https://img.fengqigang.cn//img/20210404094640.png)

### 如何查看 **ls** 是否是 **bash** 的内置命令?

**type ls**

**type -a ls**

![20210404095838](https://img.fengqigang.cn//img/20210404095838.png)

### 在 **bash** 中如何将光标移动到整个指令串的最前面或最后面?

**[ctrl] + a** 移动到最前面


**[ctrl] + e** 移动到最后面

### 如何输出 **PATH** 这个变量?

**echo ${PATH}**

![20210404102418](https://img.fengqigang.cn//img/20210404102418.png)

### 如何定义一个变量 **name**， 其内容为 **VBird** ?

```bash
name=VBird
echo ${name}
```

![20210404102857](https://img.fengqigang.cn//img/20210404102857.png)

### 如何定义一个变量 **name**， 其内容为 **VBird's name**

中间不能出来空格

```bash
name="VBird's name"
echo ${name}
```

![20210404103206](https://img.fengqigang.cn//img/20210404103206.png)

### 如何在 **PATH** 中累加 **:/home/feng/bin** 这个目录?

```bash
PATH=${PATH}:/home/feng/bin
```

![20210404103417](https://img.fengqigang.cn//img/20210404103417.png)

### 什么是Shell中的子程序?

在目前这个 **shell** 的情况下，去启用一个新的 **shell** , 新的那个 **shell** 就是子程序

一般的状态下，父程序的自订变量是无法在子程序内使用的。

但是通过 **export** 将变量变成环境变量后，就能够在子程序下面应用了

### ![20210404103835](https://img.fengqigang.cn//img/20210404103836.png) 最后一行命令可以输出吗?

不可以

一般的状态下，父程序的自订变量是无法在子程序内使用的。

但是通过 **export** 将变量变成环境变量后，就能够在子程序下面应用了

![20210404103940](https://img.fengqigang.cn//img/20210404103940.png)

### 如何进入当前核心模块目录?

uname -r 

uname - print system information

- r, --kernel-release

print the kernel release

```bash
cd /lib/modules/$(uname -r)/kernel
```

![20210404104248](https://img.fengqigang.cn//img/20210404104248.png)

### ![20210404113619](https://img.fengqigang.cn//img/20210404113619.png) 如何取消设置这个 **name**?

unset name

![20210404104409](https://img.fengqigang.cn//img/20210404104409.png)

### 如何输出环境变量与常见环境变量的说明?

```bash
env
```

![20210404104953](https://img.fengqigang.cn//img/20210404104953.png)

### 如何在 **bash** 中生成一个 **0~32767** 的数?

```bash
ehco ${RANDOM}
```

### 如何在 **bash** 中生成一个 **0~9** 之间的数值?

```bash
declare -i number=${RANDOM}*10/32768 ; echo $number;
```

![20210404105709](https://img.fengqigang.cn//img/20210404105709.png)


### 在bash 中 $ 表示的是什么?

表示这个 **Shell** 中的 **PID**

```bash
ehco $$
```

![20210404110642](https://img.fengqigang.cn//img/20210404110642.png)

### 在**bash** 中 ? 表示的是什么?

**?** 表示是上一个执行所回传的值

```bash
echo $?
```

![20210404110830](https://img.fengqigang.cn//img/20210404110830.png)

如果成功执行该指令，则会回传一个0值

### 在 **bash** 中什么是父程序? 什么是子程序?

**bash** 就量一个独立的程序

这个程序的识别使用的是一个称为程序识别码, **PID**

在这个 **bash** 下面所下达的任何指令都是由这个 **bash** 所衍生出来的，那些被下达的指令就被称为 **子程序**

![20210404111635](https://img.fengqigang.cn//img/20210404111635.png)

### 程序与变量之间有什么关系?

子程序**仅会继承父程序的环境变量**, **不会继承父程序的自订变量**

通过 **export** 指令， 可以让该变量内容继续在子程序中使用

### 如何查看系统中支持了多少的语系?

**locale -a**

![20210411091809](https://img.fengqigang.cn//img/20210411091809.png)

### 为什么在 **tty1 ~ tty6** 环境下，如何设置 **LANG=zh_CN.utf8** 这个设置值生效后，使用 **ls -l** 这个参数时，还是会出现乱码?

因为 **Linux** 主机的终端机接口环境下是无法显示像中文这么复杂的编码文字

需要再 **加装一些中文化接口的软件** 才可以看到中文

### 整体系统默认的语系定义在哪里?

**/etc/locale.conf**

![20210411092348](https://img.fengqigang.cn//img/20210411092348.png)

### 若原本是中文语系，所有显示的数据通通是中文，但为了网页显示的关系，需要将输出转成英文(en_US.utf8)的语系来展示才行, 应该如何做?

```bash
locale

LANG=en_US.utf8; locale
```

### 为什么环境变量的数据可以被子程序所引用呢?


1. 当启动一个 **shell**, 操作系统会分配一记忆区块给 **shell** 使用，此内存内这变量可让子程序取用

2. 若在父程序利用 **export** 功能， 可以让自订变量的内容写到上述的记忆区块当中(环境变量)

3. 当载入另一个 **shell** (启动子程序，离开原本的父程序), 子 **shell** 可以将父 **shell** 的环境变量所在的记忆区块导入自己的环境变量区块当中

### 如何让使用者由键盘输入一内容，将该内容变成名为 **atest** 变量?

```bash
read atest
```

![20210411093418](https://img.fengqigang.cn//img/20210411093418.png)

### 如何提示使用者 30 秒内输入自己的名字，将该输入字符串作为名为 **named** 的变量内容?

```bash
read -p "Please keyin your name:" -t 30 named
```

![20210411095904](https://img.fengqigang.cn//img/20210411095904.png)

### 在 **bash** 里 进行 **100+300+50** 的加总结果?

```bash
declare -i sum=100+300+50
echo ${sum}
```

![20210411100059](https://img.fengqigang.cn//img/20210411100059.png)

**-i to make NAMEs have the integer attribute**

### 如何将 **sum**, 改成只读属性，不可更动?

```bash
declare -r sum
```

![20210411175611](https://img.fengqigang.cn//img/20210411175611.png)

**-r to make NAMEs readonly**

### 如何查看系统内置命令的帮助?

**help 命令**

如:

**help declare**

### 设置一个数组**var[1] ~ var[3]** , 其值分别为 **small min**, **big min**, **nice min**, 并输出它

```bash
var[1]="small min"
var[2]="big min"
var[3]="nice min"
echo "${var[1]}, ${var[2]}, ${var[3]}"
```

![20210411180206](https://img.fengqigang.cn//img/20210411180206.png)

### 如何查看当前身份所有限制数据数值?

**ulimit -a**

![20210411180408](https://img.fengqigang.cn//img/20210411180408.png)

### 如何限制使用都仅能创建 **10MBytes** 以下的容量的文件?

**ulimit -f 10240**

-f

Set (or report, if no blocks operand is present), the file size limit in blocks. The -f option shall also be the default case

![20210411183933](https://img.fengqigang.cn//img/20210411183933.png)

![20210411184153](https://img.fengqigang.cn//img/20210411184153.png)

### 若账户设置了 **ulimit** , 如何取消?

登出再登陆

**一般用户者如果以ulimit设置了-f的大小，那么它只能继续减小文件大小，不能增加文件大小**

### 如何自定一个小写的 **path** 与 **PATH** 内容相同?

```bash
path=${PATH}
echo ${path}
```

![20210411184632](https://img.fengqigang.cn//img/20210411184632.png)

### ![20210411184632](https://img.fengqigang.cn//img/20210411184632.png)如果不喜欢 **local/bin** , 如何将其删除并输出?

```bash
${variable#/*local/bin:}
```

![20210411185048](https://img.fengqigang.cn//img/20210411185048.png)

### ![20210411184632](https://img.fengqigang.cn//img/20210411184632.png)如何删除最前面的一个目录?

一个 **#** 代表删除最短的那个

```bash
${variable#/*:}
```

![20210411185458](https://img.fengqigang.cn//img/20210411185458.png)

### ![20210411184632](https://img.fengqigang.cn//img/20210411184632.png)如何删除最前面的所有目录,仅保留最后一个?

两个 **##** 代表删除最长的那个

```bash
o${variable##/*:}
```

![20210411185628](https://img.fengqigang.cn//img/20210411185628.png)

### ![20210411191219](https://img.fengqigang.cn//img/20210411191219.png) 如何将 path 中的 **sbin** 转成 **SBIN**, 只替换一次?

**${变量/旧字串/新字串}**

```bash
echo ${path/sbin/SBIN}
```

![20210411191322](https://img.fengqigang.cn//img/20210411191322.png)


### ![20210411191219](https://img.fengqigang.cn//img/20210411191219.png) 如何将 path 中的 **sbin** 转成 **SBIN**, 全替换?

**${变量/旧字串/新字串}**

```bash
echo ${path//sbin/SBIN}
```

![20210411191524](https://img.fengqigang.cn//img/20210411191524.png)

### ![20210411191745](https://img.fengqigang.cn//img/20210411191745.png) 如何删除feng前面所有内容?

也就是删除/ 与 / 的所有内容

```bash
echo ${MAIL##/*/}
```

![20210411191958](https://img.fengqigang.cn//img/20210411191958.png)

### ![20210411191745](https://img.fengqigang.cn//img/20210411191745.png)如何只保留文件名?

```bash
echo ${MAIL%/*}
```

![20210411192146](https://img.fengqigang.cn//img/20210411192146.png)

### ![20210411192615](https://img.fengqigang.cn//img/20210411192615.png) 如何从后往前删除删除到第一个 **bin:**

![20210411192720](https://img.fengqigang.cn//img/20210411192720.png)

### 如何测试 **username** 这个变量， 若 **不存在** 则给予 **username** 内容为 **root**?

加上 **-**

```bash
username=${username-root}
```

![20210411192933](https://img.fengqigang.cn//img/20210411192933.png)

### 如何测试 **username** 这个变量， 若 **不存在** 或 **空字串** 则给予 **username** 内容为 **root**?

加上 **:-**

```bash
username=${username:-root}
```

### 如何判断str是否存在, 不存在则 **var** 的测试结果直接显示 **无此变量**?

```bash
var=${str?无此变量}
```

![20210411193836](https://img.fengqigang.cn//img/20210411193836.png)

### 如何判断str是否存在, 存在则 **var** 与 **str** 相同?

```bash
str="oldvar"; var=${str?novar}
echo "var=${var}, str=${str}"
```

![20210411194122](https://img.fengqigang.cn//img/20210411194122.png)

### 如何查看当前系统所有的别名?

```bash
alias
```

![20210411194528](https://img.fengqigang.cn//img/20210411194528.png)

### 如何使用 **vim** 就能打开 **nvim**?

alias vim='nvim'

![20210411194815](https://img.fengqigang.cn//img/20210411194815.png)

### 如何 **取消使用** **vim** 就能打开 **nvim**

unalias vim

![20210411195005](https://img.fengqigang.cn//img/20210411195005.png)

### **命令别名** 与 **变量** 有什么不同?

**命令别名**

新创一个新的指令，可以直接下达该指令

**变量**

需要 **echo** 指令才能调用出变量的内容

### 如何列出目前内存内所有 **history** 记忆?

**history**

![20210411195455](https://img.fengqigang.cn//img/20210411195455.png)

### 如何列出最近输入过以sudo为开头的指令?

```bash
!sudo
```

![20210411195635](https://img.fengqigang.cn//img/20210411195635.png)

### 如何执行上一个指令?

```bash
!!
```

![20210411195710](https://img.fengqigang.cn//img/20210411195710.png)

### 如何执行第66行指令?

```bash
!66
```

![20210411195808](https://img.fengqigang.cn//img/20210411195808.png)

### 若同时开好几个 **bash** 接口，这些 **bash** 的身份都是 **root**, 这样会有**~/.bash_history** 的写入问题吗?

有, 因为这些 **bash** 在同时以 **root** 的身份登陆，因此所有的 **bash** 都有自己的 1000 笔记录在内存中

等到登出时才会更新记录文件，所以，最后登出的那个 **bash** 才会是最后写入的数据






