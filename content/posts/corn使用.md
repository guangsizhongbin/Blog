---
title: "Corn使用"
date: 2021-01-12T20:34:08+08:00
lastmod: 2021-01-12
author: "xiaonan"
math:
 enable: true

tags: [corn]
categories: [linux]
---
## Install cron[^archlinux]
[^archlinux]: [Cron-Archwiki](https://wiki.archlinux.org/index.php/Cron)

`sudo pacman -S cronie`

## Quick running

### config

#### setting default Editor

`export EDITOR=/usr/bin/nvim`


#### systemctl

`systemctl enable cronie.service`

`systemctl start cronie.service`

### create cron job[^youtube]
[^youtube]: [Linux/Mac Tutorial: Cron Jobs - How to Schedule Commands with crontab](https://www.youtube.com/watch?v=QZJ1drMQz1A)

1. crontab -e

2. ![](https://img.fengqigang.cn//img/20201105163753.png)

3. Crontab format[^archlinux]


| Symbol |                         Description                        |
|:------:|:----------------------------------------------------------:|
|    *   |      Wildcard, specifies every possible time interval      |
|    ,   |         List multiple values separated by a comma.         |
|    -   | Specify a range between two numbers, separated by a hyphen |
|    /   |        Specify a periodicity/frequency using a slash       |

4. example
	
	- run every ten minutes

		*/10 * * * * echo 'Hello' >> /tmp/test.txt

	- run every hours from 1-5 am

		0 1-5 * * * * echo 'Hello' >> /tmp/test.txt

	- run every 30 minutes Mon-Fri 9am-5pm

		*/30 9-17 * * 1-5 echo 'Hello' >> /tmp/test.txt


### command

1. user

`crontab -u user`

2. list

`crontab -l`

3. remove

`crontab -r`

