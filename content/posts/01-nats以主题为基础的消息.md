---
title: "01 Nats以主题为基础的消息"
date: 2021-08-26T22:58:12+08:00
lastmod: 2021-08-26
author: "xiaonan"
math:
 enable: true

tags: 
- nats
- 消息中间件

categories: 
- nats
---

## 主题的等级

用`.`去区分不同的等级

```
time.us
time.us.east
time.us.east.atlanta
time.eu.east
time.eu.warsaw
```

## 通配符

1. `*` 匹配一个 token

如 `time.*.east` 可以匹配 `time.us.east` 和 `time.eu.east`

![20210826194451](https://img.fengqigang.cn//img/20210826194451.png)

2. `>` 匹配多个 tokens

如 `time.us.>` 可以匹配 `time.us.east` 和 `time.us.east.atlanta`

![20210826194724](https://img.fengqigang.cn//img/20210826194724.png)

3. 混合`*`与`>`

如`*.*.east.>` 可以匹配 `time.us.east.atlanta`





