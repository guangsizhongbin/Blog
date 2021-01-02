---
title: "SHH地址和HTTPS地址相互转换"
date: 2021-01-02T07:43:29+08:00
tags: [git]
categories: [git]
---

## 为什么需要转换SHH地址和HTTPS?

1. SSH地址在`push`, `pull`时均不需要输入账号密码

<!--more-->

## SHH地址的特征

![](https://img.fengqigang.cn//img/20210102083933.png)

`git@远程仓库域名:用户名/仓库名.git`

## HTTPS地址的特征

![](https://img.fengqigang.cn//img/20210102084158.png)

`https://远程仓库域名/用户名/仓库名.git`

## HTTPS地址向git地址转化

修改项目的`.git` -> `config`

![](https://img.fengqigang.cn//img/20210102084518.png)

url = git@github.com:guangsizhongbin/Blog.git

![](https://img.fengqigang.cn//img/20210102084818.png)

## 参考
[Github SSH地址和HTTPS地址的相互转换](https://lanlan2017.github.io/blog/9f3d9944/)
