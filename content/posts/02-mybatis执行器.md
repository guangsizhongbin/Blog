---
title: "02 Mybatis执行器"
date: 2021-09-13T22:39:42+08:00
lastmod: 2021-09-14
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


### 执行器

1. 简单执行器(SimpleExecutor)

无论SQL是否一样，每次都会进行预编译

2. 可重用执行器(ReuseExecutor)

相同的SQL只进行一次预处理

3. 批处理执行器(Batch Executor)

批处理提交修改

必须执行flushStatements才会生效


