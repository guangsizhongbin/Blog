---
title: "删除手机内置app"
date: 2021-01-15T20:57:29+08:00
lastmod: 2021-01-15
author: "xiaonan"
math:
 enable: true

tags: [android]
categories: [android]
---

1. 下载adb

`sudo pacman -S adb`

2. 查看当前连接的设备

`adb devices`

授权后，由`unauthorized`变成如图

![](https://img.fengqigang.cn//img/20210115210219.png)

3. 查看当前所有软件

`adb shell pm list packages`

![](https://img.fengqigang.cn//img/20210115210538.png)

4. 以删除`美团`为例子
	
- 搜索软件

	`adb shell pm list packages | grep meituan`
	
![](https://img.fengqigang.cn//img/20210115210808.png)

- 删除软件

1. 进入交互模式

	`adb shell`

![](https://img.fengqigang.cn//img/20210115210940.png)

2. 卸载软件

	`pm uninstall -k --user 0 com.sankuai.meituan`

![](https://img.fengqigang.cn//img/20210115211115.png)

{{< admonition tip>}}

`-k`: keep the data and cache directories

`--user 0`: Where 0 is ID of main user in Android system. This way you don't need to root your device.

{{< /admonition >}}[^user]

[^user]:[stack overflow: adb uninstall failed](https://stackoverflow.com/questions/13534935/adb-uninstall-failed)



