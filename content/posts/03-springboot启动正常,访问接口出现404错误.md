---
title: "03 Springboot启动正常,访问接口出现404错误"
date: 2021-09-11T23:48:34+08:00
lastmod: 2021-09-11
author: "xiaonan"
math:
 enable: true

tags:
- spring
categories:
- spring
---

## 错误事例

![20210831225748](https://img.fengqigang.cn//img/20210831225748.png)

## 产生的原因

1. `controller` 控制类不在启动类所在的目录下或子目录中

![20210831230016](https://img.fengqigang.cn//img/20210831230016.png)

## 解决的方案

1. 将启动类与`controller`放在同一层，或将`contrller`的子目录下

![20210831230725](https://img.fengqigang.cn//img/20210831230725.png)

2. 在启动类上加上`@ComponentScan(basePackages = {"cn.fengqigang.*"})` 注解


![20210831231440](https://img.fengqigang.cn//img/20210831231440.png)

也可以直接写

![20210831231618](https://img.fengqigang.cn//img/20210831231618.png)






