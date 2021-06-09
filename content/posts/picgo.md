---
title: "Picgo"
date: 2021-06-09T16:04:58+08:00
lastmod: 2021-06-09
author: "xiaonan"
math:
 enable: true

tags: [picgo]
categories: [分享]
---

### 什么是PicGo?

<div align=center>
<img src="https://img.fengqigang.cn//img/20210609143149.png" width="150" height="150" />
</div>


[github](https://github.com/Molunerfinn/PicGo)

### 如何安装PicGo?

![](https://img.fengqigang.cn//img/20210609143954.png)

#### win


- exe 安装


- choco 安装

```
choco install picgo
```

- scoop 安装

```
coop bucket add helbing https://github.com/helbing/scoop-bucket & scoop install picgo
```

#### Linux

- arch

```
yay -S picgo-appimage
```

- AppImage

```
chomod a+x PicGo-2.3.0-beta.6.AppImage
./PicGo-2.3.0-beta.6.AppImage
```

#### MacOS

- brew

```
brew install picgo --cask
```

### PicGo + 阿里云oss?[option]

1. 进入阿里云oss

![20210609145233](https://img.fengqigang.cn//img/20210609145233.png)

2. 创建一个bucket

![20210609145407](https://img.fengqigang.cn//img/20210609145407.png)

3. 填写信息

![](https://img.fengqigang.cn//img/20210609145959.png)

4. 使用单独的用户来管理oss

![](https://img.fengqigang.cn//img/20210609150309.png)

![](https://img.fengqigang.cn//img/20210609150420.png)

![](https://img.fengqigang.cn//img/20210609150541.png)

![](https://img.fengqigang.cn//img/20210609150647.png)

5. 添加权限

![20210609150824](https://img.fengqigang.cn//img/20210609150824.png)

![](https://img.fengqigang.cn//img/20210609150926.png)

![20210609150952](https://img.fengqigang.cn//img/20210609150952.png)

6. 配置picgo

![](https://img.fengqigang.cn//img/20210609151337.png)



### PicGo + 自定义域名?[option]

![](https://img.fengqigang.cn//img/20210609151607.png)

### PicGo + typora?[option]

[typora.io](https://support.typora.io/Upload-Image/#picgoapp-chinese-language-only)


![](https://img.fengqigang.cn//img/20210609151926.png)

![](https://img.fengqigang.cn//img/20210609152010.png)

![](https://img.fengqigang.cn//img/20210609152049.png)


### PicGo + nvim?[option]

[coc-picgo](https://github.com/PLDaily/coc-picgo)
[coc](https://github.com/neoclide/coc.nvim)
[neovim](https://github.com/neovim/neovim)
[vim-plug](https://github.com/junegunn/vim-plug)



1. install coc-picgo

![](https://img.fengqigang.cn//img/20210609152228.png)

2. map

![](https://img.fengqigang.cn//img/20210609152904.png)


![20210609152300](https://img.fengqigang.cn//img/20210609152300.png)

3. config

![20210609152723](https://img.fengqigang.cn//img/20210609152723.png)

![](https://img.fengqigang.cn//img/20210609152801.png)





