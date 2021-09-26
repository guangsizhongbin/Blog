---
title: "11 StatementHandle的定义与结构"
date: 2021-09-26T20:57:45+08:00
lastmod: 2021-09-26
author: "xiaonan"
math:
 enable: true

tags:
- mybatis
categories:
- mybatis
---

## StatementHandler定义

JDBC处理器，基于JDBC构建Statement, 并设置参数，然后执行Sql. 每调用会话当中一次SQL, 都会有与之相对应的且唯一的Statement的实例


## StatementHandler的结构

![20210922212043](https://img.fengqigang.cn//img/20210922212043.png)


