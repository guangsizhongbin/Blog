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

在目前这个 **shell** 的情况下，去启用一个新的 **shell** , 新的那个 **shell** 就量子程序

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

### 如何取消设置这个 **name**?

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

