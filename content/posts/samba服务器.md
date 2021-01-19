---
title: "Samba服务器"
date: 2021-01-19T21:00:08+08:00
lastmod: 2021-01-19
author: "xiaonan"
math:
 enable: true

tags: [samba]
categories: [树莓派]
---

## 安装samba
```bash
sudo apt-get update
sudo apt-get intall samba samba-common-bin
```

## 配置smb.conf

`/etc/samba/smb.conf`

```
[share]
path = /home/pi
valid users = pi
browseable = yes
public = yes
writable = yes
```

## 重新运行smaba服务

`sudo /etc/init.d/samba restart`

## 添加pi用户为Samba用户

`sudo smbpasswd -a pi`

## 参考

[树莓派4设置Samba的最新版本](https://www.jianshu.com/p/5de3a2e688b4)

[树莓派3-搭建SAMBA服务器](https://www.ncnynl.com/archives/201608/738.html)

