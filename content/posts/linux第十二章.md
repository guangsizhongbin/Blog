---
title: "Linux第十二章"
date: 2021-04-24T15:05:24+08:00
lastmod: 2021-04-24
author: "xiaonan"
math:
 enable: true

tags: [linux]
categories: [鸟哥的私房菜]
---

### 写 Shell Script 的规则是什么?

1. 第一行写 #!/bin/bash 来宣告这个文件内的语法使用的是 **bash** 语法

2. 程序内容的说明:

- 内容与功能
- 版本信息
- 作者与联络方式
- 创建日期
- 历史记录

3. 主要环境变量的宣告 **PATH** 与 **LANG**

4. 执行成果告知

```bash
exit 0
```

当下达 

```bash
echo $? 
```

则可得到0的值

![20210424143200](https://img.fengqigang.cn//img/20210424143200.png)

### echo -e 会发生什么?

- e

enable interpretation of backslash escapes

### 以 **read** 指令的用途，撰写一个 **script**, 他可以让使用者输入 1. first name 与 2. last name, 最后并且在屏幕上显示 "Your full name is:" 的内容?

```bash
#!/bin/bash
# Program:
# User input his first name adn last name. Program shows his full name.
# Histroy:
# 2015/07/16		feng		First relase
PATH=/usr/local/sbin:/usr/local/bin:/usr/bin:/usr/lib/jvm/default/bin:/usr/bin/site_perl:/usr/bin/vendor_perl:/usr/bin/core_perl

export PATH

read -p "Please input your first name: " firstname # 提示使用者输入
read -p "Please input your last name: " lastname # 提示使用者输入
echo -e "\nYour full name is: ${firstname} ${lastname}" # 结果由屏幕输出
```

-p prompt

print the prompt text before requesting the input from the standard input stream without a <newline> character.

### 如何创建三个空文件，文件名最开头由使用者输入决定，假设使用者输入 filename 好了, 我想以前天，昨天，今天的日期来创建这些文件?

```bash
#!/bin/bash
# Program:
#		Program creates three files, which named by user's input and date command.
# History:
# 2015/07/16	feng	First release
PATH=/usr/local/sbin:/usr/local/bin:/usr/bin:/usr/lib/jvm/default/bin:/usr/bin/site_perl:/usr/bin/vendor_perl:/usr/bin/core_perl
export PATH

# 1. 让使用者输入文件名称，并取得 fileuser 这个变量
echo -e "I will use 'touch' command to create 3 files" 
read -p "Please intput your filename: " fileuser

# 2. 利用变量功能，避免使用者随意按 Enter
filename=${fileuser:-"filename"}

# 3. 开始利用 data 指令来取得所需要的文件名
date1=$(date --date='2 days ago' +%Y%m%d)
date2=$(date --date='1 days ago' +%Y%m%d)
date3=$(date +%Y%m%d)
file1=${filename}${date1}
file2=${filename}${date2}
file3=${filename}${date3}

# 4. 将文件名创建
touch "${file1}"
touch "${file2}"
touch "${file3}"
```


