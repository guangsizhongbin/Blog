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


### 如何将 **ehco** 命令别名成 **echo -n**? 再观察 **ehco** 的执行顺序?

```bash
alias echo='echo -n'

type -a echo
```

![20210414142147](https://img.fengqigang.cn//img/20210414142147.png)

### 如何查看 **bash** 进站时的画面与欢迎信息?

```bash
cat /etc/issue
```

![20210414143031](https://img.fengqigang.cn//img/20210414143031.png)

### 如何查看 **/etc/issue** 文件中各种参数?

**man issue** 与 **man agetty**

### 如何想要让使用者登陆后取得一些讯息，例如想要让大家都知道的讯息，那么可以将讯息加入 **/etc/motd** 里面去

vim /etc/motd

motd - message of the day

The contents of **/etc/motd** are displayed by login after a successful login but just before it executes the login shell.

### 什么是 **login shell** 和 **non-login shell**, 如何区分它们?

**login shell** 与 **non-login shell** 区别在于有没有登录

**login shell**

取得 **bash** 时需要完整的登录流程

**non-login shell** 

取得 **bash** 接口的方法不需要登陆的举动

### **login shell**  与 **non-login shell** 有什么不同?

**login shell** 只会读取两个配置文件

1. **/etc/profile**

系统整体的设置

2. **~/.bash_profile** 或 **~/.bash_login** 或 **~/.profile**

属于个人设置

**non-login shell** 仅会读一个文件

1. **~/.bashrc**

### 有哪些例子是用 **non-login shell** 的?

1. 以 **X window** 登陆 **Linux** 后，再以 **X** 的图形化接口启动终端机，此时那个终端接口并没有需要再次的输入账号与密码，那个 **bash** 环境被称为 **non-login shell** 了

2. 在原本的 **bash** 环境再次下达 **bash** 这个指令，同样的也没有输入账号密码，那第二个 **bash** (子程序) 也是 **non-login shell**

### 若不小心将 **~/.bashrc** 删除了，如何恢复?

复制 **/etc/skel/.bashrc** 到主文件夹中, 并使用 **source** 去调用

### **~/.bash_logout** 文件是用来干什么的?

默认的情况下，登出时，**bash** 只是帮我们清楚屏幕信息而已

可以将一些备份或者是其他重要的工作写在这个文件中

### **~/.bash_history** 文件是用来干什么的?

默认的情况下，历史命令就记录在这里

而这个文件能够记录几笔数据，与 **HISTFILESIZE** 这个变量有关

### 如何列出所有的按键与按键内容?

**stty -a**

![20210414152328](https://img.fengqigang.cn//img/20210414152328.png)

### 在 **window** 下面，很多软件默认的储存快捷按钮是 **[Ctrl] + s**, 在 **linux** 下面使用 **vim** 时， 按下 **[Ctrl] + s** 就不动了，该如何做?

**[Ctrl] + s** 是 **stop**

**[Ctrl] + q** 是 **start**


![20210414152628](https://img.fengqigang.cn//img/20210414152628.png)

### 如何显示目前所有的 **set** 设置值?

```bash
echo $-
```

![20210414153031](https://img.fengqigang.cn//img/20210414153031.png)

### 如何找出 **/etc/** 下面文件名 **刚好是一个字母** 的文件名?

```bash
ll -d /etc/?????
```

![20210414153256](https://img.fengqigang.cn//img/20210414153256.png)

### 如何找出 **/etc** 下面文件含有数字的文件名?

```bash
ll -d /etc/*[0-9]*
```

### 如何找出 **/etc/** 下面文件名开头为非小写字母的文件?

```bash
ll -d /etc/[^a-z]*
```

### **find /home -name .bashrc > list_right 2> list_error** 这句是什么意思?

**>** 标准输出 (stdout)

**2>** 标准错误输出 (stderr)

将找到的到至 **list_right** 中

错误放到 **list_error** 中

### **find /home -name *bashrc 2> /dev/null** 这句会什么意思?

**2>** 标准错误输出 (stderr)

**/dev/null** 可以吃掉任何导向这个设备的信息

直接会把错误的信息丢弃

### 如何将 **find /home -name .bashrc** 这语的正确和错误信息全输出到 list?

**2>&1** 和 **&>** 都可以

```bash
find /home -name .bashrc > list 2>&1
```

```bash
find /home -name .bashrc &> list
```

### 如何我想用 **cat**  直接将输入的讯息输出到 **catfile** 中， 且当由键盘输入 **eof** 时, 这次输入就结束了, 可以怎么做?

```bash
cat > catfile << "eof"
```

<< 表示 **结束的输入字符** 的意思

![20210417141949](https://img.fengqigang.cn//img/20210417141949.png)

### **cat > catfile < ~/.bashrc** 是什么意思?

会将 **~/.bashrc** 作为输入流， 输入到 **catfile** 中

### **ls /tmp/abc && touch /tmp/abc/hehe** 是什么意思?

查阅 **/tmp/abc** 是否存在，若存在则用 **touch** 创建 **/tmp/abc/hehe**

![20210417142551](https://img.fengqigang.cn//img/20210417142551.png)

### **ls /tmp/abc || mkdir /tmp/abc** 是什么意思?

判断 **/tmp/abc** 是否存在， 如何不存在则创建，若存在就不作任何事情

### 如果我不清楚 **/tmp/abc** 是否存在, 但就是要创建 **/tmp/abc/hehe** 文件? 为什么?

```bash
ls /tmp/abc || mkdir /tmp/abc && touch /tmp/abc/hehe
```

1. 

若 **/tmp/abc** 不存在所以加传 $?!=0, 

由因为 || 遇到非 0 的 $? 故 mkdir /tmp/abc, 

由于 mkdir /tmp/abc 会成功进行, 所以回传 $?=0, 

因为 && 遇到 $?=0 故会执行 touch /tmp/abc/hehe, 最终 hehe 就被创建了

2. 

若 **/tmp/abc** 存在故回传 $?=0
 
由因为 || 遇到 0 的 $? 不会继续向后传

因为遇到 $?=0 就开始创建 **/tmp/abc/hehe** 了

![20210417144047](https://img.fengqigang.cn//img/20210417144047.png)

### 以 ls 测试 /tmp/vbirding 是否存在， 若存在则显示 "exist", 若不存在， 则显示 "not exist"

```bash
ls /tmp/vbirding && echo "exist" || echo "not exist"
```

![20210417144340](https://img.fengqigang.cn//img/20210417144340.png)

### **ls /tmp/vbirding || echo "not exitst" && echo "exist"** 的执行会出现什么问题?

1. 若 **ls /tmp/vbirding** 不存在， 因此回传一个非为0的数值

2. 经过 **||** 的判断，发现前一个指令回传非为0的值，因此，程序开始执行 echo "not exist" , 而 echo "not exist" 程序肯定执行成功，因此会回传一个0值后面的指令

3. 经过 && 的判断， 是0, 所以就开始执行 echo "exist"

![20210417144840](https://img.fengqigang.cn//img/20210417144840.png)


### 当假设判断式有三个时候，一般如何去排布?

command 1 && command 2 || command 3

### 管道命令 **|** 有什么特点?

仅能处理经由前面一个指令传来的正确信息，也就是 **standard output**

对于 **stdandard error** 并没有直接处理的能力

![20210417145205](https://img.fengqigang.cn//img/20210417145205.png)

### **echo ${PATH} | cut -d ':' -f 5** 是什么意思?

cut:

remove sections from each line of files

**-d, --delimiter=DELIM**

use DELIM instead of TAB for field delimiter

**-f, --fields=LIST**

select only these fields; also print any line that contains no delimiter character, unless the -s option is specified.

![20210417145628](https://img.fengqigang.cn//img/20210417145628.png)

###  如何只想看到 export 中第12个字符以后的字符应该如何处理?

```bash
export | cut -c 12-
```

cut:

remove sections from each line of files

**-c, --characters=LIST**

select only these characters

![20210417150110](https://img.fengqigang.cn//img/20210417150110.png)

### 如何用 **last** 显示登录者的信息中, 仅留下使用者的大名?![20210417155137](https://img.fengqigang.cn//img/20210417155137.png)

**last | cut -d ' ' -f 1**



![20210417190812](https://img.fengqigang.cn//img/20210417190812.png)

### 如何使用 **last** 找出没有 **root** 的行?

last | grep -v 'root'

-v, --invert-match

Invert the sense of matching, to select non-matching lines.

![20210417190956](https://img.fengqigang.cn//img/20210417190956.png)

### 如何使用 **last** 找出没有 **root** 的行, 并且只取第一栏?

last | grep -v 'root' | cut -d ' ' -f1

![20210417191320](https://img.fengqigang.cn//img/20210417191320.png)

### 如何取 **/etc/man_db.conf** 内含 **MANPATH** 的那行? 并实现自动语法高亮?

grep --color=auto 'MANPATH' /etc/man_db.conf

![20210417191807](https://img.fengqigang.cn//img/20210417191807.png)

### 如何对 **/etc/passwd** 的文件内容进行排序?

cat /etc/passwd | sort

![20210417191747](https://img.fengqigang.cn//img/20210417191747.png)

### 如何对 **/etc/passwd** (以 : 分隔), 如何以第三栏来排序?

cat /etc/passwd | sort -t ':' -k 3

-t, --field-separator=SEP

use SEP instead of non-blank to blank transition

-k, --key=KEYDEF

sort via a key; KEYDEF gives location and type

![20210417192101](https://img.fengqigang.cn//img/20210417192101.png)

### 如何利用 last , 将输出的数据仅取账号，并加以排序?

last | cut -d  ' ' -f1 | sort

-d, --delimiter=DELIM

use DELIM instead of TAB for field delimiter

![20210417192419](https://img.fengqigang.cn//img/20210417192419.png)

### 如何利用 last , 将输出的数据仅取账号，并加以排序, 排序后仅取出一位?

last | cut -d ' ' -f1 | sort | uniq

uniq

report or omit repeated lines

![20210417192626](https://img.fengqigang.cn//img/20210417192626.png)

### 如何利用 last , 将输出的数据仅取账号，并加以排序, 排序后仅取出一位, 并统计出现的个数?

last | cut -d ' ' -f1 | sort | uniq -c

uniq

report or oomit repeated lines

-c, --count

prefix lines by the number of occurrences

![20210417192924](https://img.fengqigang.cn//img/20210417192924.png)

###  如何统计 /etc/man_db.conf 里面有多少相关字、行、字符数?

cat /etc/man_db.conf | wc

wc

print newline, word, and byte counts for each file

![20210417193210](https://img.fengqigang.cn//img/20210417193210.png)

### last 可以输出登录者，但是 last 最后两行并非账号内容，如何以一行指令串取得登录系统的总人次?

last | grep [a-zA-Z] | grep -v 'wtmp' | grep -v 'reboot' | grep -v 'unknown' | wc -l

![20210417193647](https://img.fengqigang.cn//img/20210417193647.png)

### **tee** 命令是什么样的?

tee - read from standard input and write to standard output and files

![20210417194850](https://img.fengqigang.cn//img/20210417194850.png)

### 如何将 **last** 命令输出的内容, 存一份到 **last.list** 中， 并输出第一行的内容?

tee - read from standard input and write to standard output and files

last | tee last.list | cut -d " " -f1

![20210417194915](https://img.fengqigang.cn//img/20210417194915.png)

### 如何将 **last** 输出的讯息中，所有的小写变成大写字符?

tr - translate or delete characters

last | tr '[a-z]' '[A-Z]'

![20210417195043](https://img.fengqigang.cn//img/20210417195043.png)

### 如何将 **/etc/passwd** 输出的讯息中， 将冒号 (:) 删除?

tr - translate or delete characters

cat /etc/passwd | tr -d ':'

![20210417195228](https://img.fengqigang.cn//img/20210417195228.png)

### 如何将 **/etc/man_db.conf**  中的 [tab] 转成空白?![20210417200357](https://img.fengqigang.cn//img/20210417200357.png) 

col - filter reverse line feeds from input

-x, --spaces

Output multiple space instead of tabs.

![20210417200539](https://img.fengqigang.cn//img/20210417200539.png)

### 如何将 /etc/passwd/ 与 /etc/shadow 相关数据整合成一栏?

join -t ':' /etc/passwd /etc/shadow | head -n 3

![20210417200750](https://img.fengqigang.cn//img/20210417200750.png)

### 可以将/home/feng/Desktop/Win10_1909_Chinese(Simplified)_x64.iso 文件分成多份，1份为1个G吗?

split -b 1G /home/feng/Desktop/Win10_1909_Chinese(Simplified)_x64.iso win10

split

split a file into pieces

-b, --bytes=SIZE

put SIZE bytes per output file

Output pieces of FILE to PREFIXaa, PREFIXab, ...; default size is 1000 lines and, default PREFIX is 'x'

![20210417212613](https://img.fengqigang.cn//img/20210417212613.png)

### 如何将 win10aa ~ win10af, 合成 win10.iso?

数据流重导向即可

cat win10** >> win10.iso

### 如何使用 ls -al / 输出的信息中，每十行记录成一个文件?

ls -al / | split -l 10 - lsroot

With no FILE, or when FILE is -, read standard input.

![20210417213252](https://img.fengqigang.cn//img/20210417213253.png)

### **xargs** 是做什么的?

x 是加减乘除的乘号， args 是 arguments 参数的意思

它是产生某个指令的参数的意思

xargs 可以读入 stdin 数据， 并且以空白字符或断行字符作为分辨， 将 stdin 的数据分隔成为 arguments

### 如何将 /etc/passwd 内的第一栏取出，仅取三行，使用 id 这个指令将第个账号内容秀出来?

cut -d ':' -f 1 /etc/passwd | head -n 3 | xargs -n 1 id

-n max-args, --max-args=max-argumets per command line.

![20210417215442](https://img.fengqigang.cn//img/20210417215442.png)

### 如何将 /etc/passwd 内的第一栏取出，仅取三行，使用 id 这个指令将第个账号内容秀出来， 每次执行 id 时，都要询问使用者是否动作?

cut -d ':' -f 1 /etc/passwd | head -n 3 | xargs -p -n 1 id

-p 

xargs never terminates its commands; when asked to decres it merely waits for more than one existing command to terminate before starting another.

![20210417215506](https://img.fengqigang.cn//img/20210417215506.png)

### 将所有的 /etc/passwd 内的账号都以 id 查阅， 但查到 sync 就结束指令串?

cut -d ':' -f 1 /etc/passwd | xargs -e'sync' -n 1 id

-e eof-str

Set the end of file string to eof-str


![20210417215705](https://img.fengqigang.cn//img/20210417215705.png)

**连在一起的**

### 如何找出  /usr/sbin 下面具有特殊权限的文件名(/700)，并使用 ls -l 列出详细属性?

find /usr/sbin -perm /7000 | xargs ls -l

![20210417215248](https://img.fengqigang.cn//img/20210417215248.png)


### - 的什么用?

1. 用前一个命令的 stdout 作为这次的 stdin

**tar -cvf - /home | tar -xvf - -C /tmp/homeback**








