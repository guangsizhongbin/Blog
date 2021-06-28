---
title: "Aop"
date: 2021-06-28T23:14:37+08:00
lastmod: 2021-06-28
author: "xiaonan"
math:
 enable: true

tags: [spring]
categories: [王道]
---

### AOP编程实战

1. 引入依赖

2. 注册委托类组件

3. 提供一个通知组件并注册(MethdoInterceptor 是来自于 org.aopalliance.intercept)


![20210628195537](https://img.fengqigang.cn//img/20210628195537.png)

![20210628195705](https://img.fengqigang.cn//img/20210628195705.png)

### ASPECT 强化advisor - pointcut


![20210628204149](https://img.fengqigang.cn//img/20210628204149.png)


![](https://img.fengqigang.cn//img/20210628204231.png)


### advisor 的时间属性

1. Before

2. After

3. Around

4. AfterReturning

5. AfterThrowing

![20210628212224](https://img.fengqigang.cn//img/20210628212224.png)

![20210628213214](https://img.fengqigang.cn//img/20210628213214.png)

![20210628215101](https://img.fengqigang.cn//img/20210628215101.png)



### joinPoint 的参数

ProceedingJoinPoint extends 于 JoinPint


- getSignature() 方法信息

- getName() 方法名

- getArgs() 参数

- getThis() proxy

- getTarget() 委托类对象

![20210628214038](https://img.fengqigang.cn//img/20210628214038.png)


### CustomAspect

1. 指定组件为切面组件 @Aspect , 保留@Component

![20210628223142](https://img.fengqigang.cn//img/20210628223142.png)

2. 配置切入点 @Pointcut("execution(* cn..service..*(..))")

![20210628223249](https://img.fengqigang.cn//img/20210628223249.png)


3. @Around

![20210628223401](https://img.fengqigang.cn//img/20210628223401.png)

4. @AfterReturning @AfterThrowing

![20210628223513](https://img.fengqigang.cn//img/20210628223513.png)


