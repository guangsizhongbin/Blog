---
title: "Github Actions 自动部署hugo至vps"
date: 2021-01-01
lastmod: 2021-01-01
author: "xiaonan"

tags: ["git","hugo"]
categories: [hugo]
draft: false

---

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

## 上传Hugo源文件至Github

1. 不需要上传`public`中的文件

{{< admonition >}}
1. 不跟踪某个`public`文件夹(git status不再提醒)
	- 修改 `.gitignore`
		加入 public/

2. 对`public`文件夹取消跟踪
	- git rm -r --cached public 删除`public`文件夹的跟踪，并保留在本地
	- git rm -r --f public 删除`public`文件夹的跟踪，并且删除本地文件
{{< /admonition >}}

## Github Actions构建Hugo并用WebHook回调

### 生成Access token

个人的Settings -> Developer settings -> Personal access tokens -> Generate new token -> Generate token

![](https://img.fengqigang.cn//img/20210101165022.png)

![](https://img.fengqigang.cn//img/20210101165116.png)

![](https://img.fengqigang.cn//img/20210101165146.png)

保存好获取到的 `access token`, 它只会出现一次


### 添加Access Token到项目

项目Secrets -> New repository secret -> Add secret

![](https://img.fengqigang.cn//img/20210101165842.png)



### 宝塔安装WebHook

宝塔 -> 应用搜索 -> webhook

![](https://img.fengqigang.cn//img/20210103104150.png)

### 设置脚本


![](https://img.fengqigang.cn//img/20210103113736.png)

```shell
#!/bin/bash
echo ""
date --date='0 days ago' "+%Y-%m-%d %H:%M:%S"
echo "Start"

gitPath="/www/wwwroot/fengqigang.cn"
gitHttp="https://github.com/guangsizhongbin/Blog.git"

echo "Web站点路径:$gitPath"
if [ -d "$gitPath" ]; then
	cd $gitPath
	if [ ! -d ".git" ]; then
		echo "在该目录下克隆 git"
		git clone -b gh-pages $gitHttp gittemp
		mv gittemp/.git .
		rm -rf gittemp
	fi
	git reset --hard gh-papes
	git pull
	chown -R www:www $gitPath
	echo "End"
	exit
else
	echo "该项目路径不存在"
	echo "End"
	exit
fi
```

{{< admonition >}}
1. `date` agruments

- `--date=STRING`

		display time described by STRING, not 'now'

```bash
// 显示当前时间
$ date --date="0 days ago"
Sun Jan  3 10:54:04 AM CST 2021

// 显示2天之后的时间
$ date --date="2 days"
Tue Jan  5 10:55:14 AM CST 2021

// 显示2个星期之后的时间
$ date --date="2 weeks"
Sun Jan 17 10:55:22 AM CST 2021
```

-  `+%Y-%m-%d %H:%M:%S`
	- `%Y` year
	- `%m` month (01..12)
	- `%d` day of month (e.g., 01)
	- `%H` hour (00..23)
	- `%M` minute (00..59)
	- `%S` second (00..60)

**day of month** 是小写的d

```bash
// 显示当前时间
$ date '+%Y-%m-%d %H:%M:%S'
2021-01-03 11:07:00

// 显示当前时间
$ date --date="0 days ago" '+%Y-%m-%d %H:%M:%S'
2021-01-03 11:08:47
```

2. `git` arguments

- `-b <name>`
	
	`Instead of pointing the newly created HEAD to the branch pointed to by the cloned repository's HEAD, point to <name> brach instead.`

- `git reset --hard gh-pages`
	
	`Restes the index and working tree. Any changes to tracked files in the working tree since <commit> are discarded.`

	退回到远程仓库中的版本

{{< /admonition >}}

项目Actions -> Set up a workflow yourself -> 添加代码 -> Start commit

![](https://img.fengqigang.cn//img/20210101170313.png)

```workflow
name: Deploy Hugo # 自己命名即可

on: # 设置触发条件
	push:
		branches:
			- master # master 分支被更新时触发

job: # 设置触发时间
	build-deploy:
		runs-on: ubuntu-18.04
		steps:
			- uses: actions/checkout@v1

			- name: Setup Hugo
				uses: peaceiris/actions-hugo@v2
				with:
					hugo-version: latest

			- name: Build
				run: hugo

			- name: Deploy
				uses: peaceiris/action-gh-pages@v3
				with:
					personal_token: ${{ secrets.personal_token}}
					PUBLISH_BRANCH: gh-pages # 推送至分支名称
					PUBLISH_DIR: ./public # 将hugo 生成的 public 作为根目录
					comit_message: ${{ github.event.head_commit.message }}
```
### 将秘钥添加至项目中的Secrets

项目的`Setting` -> Secrets

![](https://img.fengqigang.cn//img/20210103113957.png)

![](https://img.fengqigang.cn//img/20210103130336.png)

### 添加Github Actions workflow 事件

```workflow
	- name: Webhook
		uses: distributhor/workflow-webhoob@v1
		env:
			webhook_url: ${{ secrets.WEBHOOK_URL }}$
			webhook_secret: ${{ secrets.WEBHOOK_SECRET }}$
```

## 参考

[Hugo + Github Actions 实现自动化部署](https://immmmm.com/hugo-github-actions/)



	
