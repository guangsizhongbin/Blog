---
title: "MergeSort"
date: 2021-01-07T16:41:56+08:00
lastmod: 2021-01-07
author: "xiaonan"
math:
 enable: true
draft: true
tags: [algorithm]
categories: [数据结构]
---

## 

## Tip

{{< admonition tip >}}

> 1. 怎么定义一个结点，并生成一个列表？

```C
typedef struct{
	int key;
}SqNode;

typedef struct{
	SqNode r[MAX];
	int length;
}SqList;

2. 如何实现`Merge`?

void Merge(SqNode SR[], SqNode TR[], int i, int m, int n){};
```

{{< /admonition >}}
