---
title: "Day37"
date: 2021-05-12T23:29:10+08:00
lastmod: 2021-05-12
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

**Shiro** 权限验证框架

### 什么是符号表(Map)



![](https://img.fengqigang.cn//img/20210512100829.png)

![](https://img.fengqigang.cn//img/20210512100959.png)



![](https://img.fengqigang.cn//img/20210512101239.png)





就是 Key-value数据 



### 互联网三要素:

**url**

怎么找到某个资源，资源位置在哪里?

**http**

描述资源在网络上的传输方式

**html**

描述论文



### 怎么在互联网上唯一表示一台计算机

ip + 地址



### url 分类三大部分

![](https://img.fengqigang.cn//img/20210512110038.png)

### 什么哈希表?

![](https://img.fengqigang.cn//img/20210512111124.png)

### Hash函数具有的特点

![](https://img.fengqigang.cn//img/20210512113248.png)

### Hash算法不是加密算法

![](https://img.fengqigang.cn//img/20210512111716.png)

加密意味着解密





主流的 hash 算法: sha1（谷歌的两个程序员）,  md5(王小云), 已经被证明不具有强抗碰撞性(先简单认为不安全)



碰撞性:

![](https://img.fengqigang.cn//img/20210512113040.png)



### 主流的 hash 函数

![](https://img.fengqigang.cn//img/20210512113352.png)



加盐： 盐值



账号: Admin

密码: 123



![](https://img.fengqigang.cn//img/20210512113758.png)





![](https://img.fengqigang.cn//img/20210512114713.png)

![](https://img.fengqigang.cn//img/20210512114744.png)

![](https://img.fengqigang.cn//img/20210512114850.png)



### 理论上的 hash 冲突如何解决?



![](https://img.fengqigang.cn//img/20210512115119.png)

线性探测法

平方探测法

再散列法



