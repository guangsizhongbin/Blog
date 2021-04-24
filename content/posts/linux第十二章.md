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




