---
title: "Day38"
date: 2021-05-13T23:34:52+08:00
lastmod: 2021-05-13
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### 为什么是出现 `html`?

当时是为了传论文


#### `html` 是谁的?

html + css + js 都是W3C的

W3C (The World Wide web Consortium)

它是一个组织， 只提供一系列的草案，因此没有相关的文档


### 为什么在不同的浏览器中执行相同的前端代码， 有些浏览器会走形, 并且错误的代码也可以输出?

因为为了在浏览器大战中获得胜利，各家的浏览器并没有完全遵循W3C的标准

同时各家的浏览器为了获得更多的市场，会包容错误代码


### 前端, 网页, Html, Css, JavaScript, 它们之间是什么样的关系?

前端: 写页面

网页: 人

Html: 骨架

Css: 皮肤和血肉

Js(JavaScript): 思想逻辑

### 什么是 `Html` ?

是一种语言

文本语言: 超文本

是一个以 `.html` 为后缀的文本

'超文本' 包括文本字体, 图片, 链接， 甚至音乐，程序等元素代码的文本

是一个文本， 也是一个网页，该文本用浏览器打开， 文本里代码会进行解释执行

### html 的标准结构是什么样的?

![](https://img.fengqigang.cn//img/20210513110907.png)

![](https://img.fengqigang.cn//img/20210513111036.png)

### html 重要的body标签

1.  块级标签
    
2.  行级标签
    
3.  行内块标签
    

### `<hr>` 标签是什么意思? 有什么需要注意的?

1. `<hr>` 是一个单标签

`<hr>` `</hr>` 是错误的



2. 不要写成 `<hr />`

`<hr />` 是 `xhtml` 的写法

`xhtml` 是用来增强 `html` 的样式功能，现在已经过时



### `<br>` 标签是用来作什么的?

1. `<br>` 是用来换行的

2. 对于一个 `html` 页面来说， 在代码中连续换行或者空格，在页面显示上仅仅会解析成一个空格

![20210516100329](https://img.fengqigang.cn//img/20210516100329.png)

这里代表的是三个空格

![20210516100418](https://img.fengqigang.cn//img/20210516100418.png)

### `html` 中可以使用 自定义的标签吗?

`html` 中可以自定义标签， 但是自定义的标签不会有任何特殊效果

![20210516100711](https://img.fengqigang.cn//img/20210516100711.png)

![20210516100750](https://img.fengqigang.cn//img/20210516100750.png)


### `<hn>`标签是用来干什么的?有什么需要注意的?

1. `<h1> - <h6>` 只有6个标签, 它是成对标签

![20210516101253](https://img.fengqigang.cn//img/20210516101253.png)

正文会比某些标签要大

![20210516101332](https://img.fengqigang.cn//img/20210516101332.png)

![](https://img.fengqigang.cn//img/20210513154759.png)

2. 在一个 `html`页面中， `h1` 标题仅能出现一次， `h2-h6` 可以出现多次

`h1` 除了显示以外， 还作为关键字

### `div` 标签是用来干什么的? 有什么需要注意的?

![](https://img.fengqigang.cn//img/20210513160129.png)

### a

![](https://img.fengqigang.cn//img/20210513160557.png)

**它的属性没法被替代**

href = "xxxxx",

![](https://img.fengqigang.cn//img/20210513161944.png)

### p

![](https://img.fengqigang.cn//img/20210513163137.png)

### img

**not alllow to load local source**

非网络请求

![](https://img.fengqigang.cn//img/20210513172705.png)

![](https://img.fengqigang.cn//img/20210513173013.png)

EE:

动态资源

静态资源

### Input

### 物理像素与虚拟像素？

![](https://img.fengqigang.cn//img/20210513143503.png)

### 页面加载流程(与服务器)

![](https://img.fengqigang.cn//img/20210514093309.png)



### 页面加载流程(本地服务器)

![](https://img.fengqigang.cn//img/20210514093445.png)



### 页面加载流程(本地服务器, 图片也在本地)

![](https://img.fengqigang.cn//img/20210514093526.png)



![](https://img.fengqigang.cn//img/20210514111949.png)

![](https://img.fengqigang.cn//img/20210514112631.png)






