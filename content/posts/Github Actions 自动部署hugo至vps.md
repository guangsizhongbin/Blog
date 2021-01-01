---
title: "Github Actions 自动部署hugo至vps"
date: 2021-01-01
lastmod: 2021-01-01
author: "xiaonan"

tags: ["git","hugo"]
categories: [hugo]

---

Password:

8!aSXVL\]Q6-7z9qG

## 系统版本

```bash
root@vultr:~# hostnamectl

  Static hostname: vultr.guest
        Icon name: computer-vm
          Chassis: vm
       Machine ID: 014b2aed70f7e09db32693a85feeb49a
          Boot ID: fe9876f6146f4fb4a3187f09d94f5ab3
   Virtualization: kvm
 Operating System: Debian GNU/Linux 9 (stretch)
           Kernel: Linux 4.9.0-14-amd64
     Architecture: x86-64

```

`我使用的是Debian 9`

## 安装宝塔

```bash
wget -O install.sh http://download.bt.cn/install/install-ubuntu_6.0.sh && bash install.sh
```

```
外网面板地址: http://141.164.50.150:8888/066aa3f1
内网面板地址: http://141.164.50.150:8888/066aa3f1
username: ikend6fd
password: 11f1caf3
```

## 添加 Github Actions 代码:

1.生成Access token

个人的Settings -> Developer settings -> Personal access tokens -> Generate new token -> Generate token

![](https://img.fengqigang.cn//img/20210101165022.png)

![](https://img.fengqigang.cn//img/20210101165116.png)

![](https://img.fengqigang.cn//img/20210101165146.png)

保存好获取到的 `access token`, 它只会出现一次

17159f0fc1815dbe5faaa86e9ccd33101e11a96f

2. 添加Access Token到项目

项目Secrets -> New repository secret -> Add secret

![](https://img.fengqigang.cn//img/20210101165842.png)

3. 部署Actions

项目Actions -> Set up a workflow yourself -> 添加代码 -> Start commit

![](https://img.fengqigang.cn//img/20210101170313.png)

## 同步到服务器



	
