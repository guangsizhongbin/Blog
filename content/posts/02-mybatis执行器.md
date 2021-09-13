---
title: "02 Mybatis执行器"
date: 2021-09-13T22:39:42+08:00
lastmod: 2021-09-13
author: "xiaonan"
math:
 enable: true

tags:
- mybatis
categories:
- mybatis
---

## mybatis的四大模块

1. 动态代理 MapperProxy

2. SQL 会话 SqlSession

3. 执行器 Executor

4. JDBC StatementHandler

![20210913223133](https://img.fengqigang.cn//img/20210913223133.png)

## Mybatis的执行过程

门面模式:

提供一个`统一的门面接口API`, 使得系统更容易使用

![20210913223517](https://img.fengqigang.cn//img/20210913223517.png)


