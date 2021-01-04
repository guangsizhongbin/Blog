---
title: "Docker"
date: 2021-01-02T19:34:39+08:00
lastmod: 2021-01-03
author: "xiaonan"

tags: [docker]
categories: [docker]
draft: false
---

## Docker 三大基本概念

`镜像`(Image)

`容器`(Container)

`仓库`(Repository)

<!--more-->

## 安装Docker(Debian)

## 镜像

### 获取镜像

`docker pull [选项] [Docker Registry 地址[:端口号]/]仓库名[:标签]`

- Docker 镜像仓库地址 默认地址是 Docker Hub(docker.io)
- 仓库名 <用户名>/<软件名> 对于`Docker Hub`, 不给出用户名，默认为`library`, 即官方镜像


比如:


```bash
docker pull mquandalle/wekan

docker pull debian //不给出用户名，使用用官方镜像

docker pull ubuntu:14.04 //使用官方镜像中版本号为14.04的ubuntu
```
{{< admonition tip >}}
Docker是采取`分层存储`的概念, 镜像是由多层存储所构成。下载也是一层层去下载，并非单一文件。

![](https://img.fengqigang.cn//img/20210102201338.png)
{{< /admonition >}}

### 运行镜像

```bash
$ docker run -it --rm ubuntu:14.04
```

参数说明：

- `-it`: `-i`:交互式操作 `-t`: 表示终端
- `--rm`: 表示容器退出后随之将其删除

### 列出镜像

```
$ docker image ls
```

![](https://img.fengqigang.cn//img/20210102202316.png)

{{< admonition tip >}}
`Docker Hub`中显示的体积与`docker image ls`显示的镜像大小不同

![](https://img.fengqigang.cn//img/20210102202847.png)

`Docker Hub`中显示的体积是压缩后的体积，在镜像下载和上传的过程中镜像是保持着压缩状态的，在网络传输过程中，关心的是流量大小

`docker image ls`列表中的镜像体积总和并非是所有镜像实际硬盘消耗。由于Docker镜像是多层存储结构，并且可以继承、复用，因此不同镜像可能会使用相同的基础镜像，从而拥有共同的层。相同的层只需要保存一份即可，因此实际镜像硬盘占用空间很可能比这个列表镜像大小的总和要小的多。

```bash
$ docker system df
```

可以查看镜像、容器、数据卷所占用的空间

![](https://img.fengqigang.cn//img/20210102203623.png)

{{< /admonition >}}

### 删除镜像

```bash
$ docker image rm [选项] <镜像1> [<镜像2>]
```

<镜像> 可以是`ID`, `镜像名`或`镜像摘要`

- `ID`: 一般取前3个字符以上，只要足够区分别的镜像就可以了

	- 如：
	`docker image rm df0`

- `镜像名`: `<仓库名>:<标签>`

	- 如：
`docker image rm mongo:latest`

- `镜像摘要`

	- ```bash
		$ docker image ls --digests
