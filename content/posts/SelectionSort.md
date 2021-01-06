---
title: "Selection_Sort"
date: 2021-01-05T19:30:27+08:00
lastmod: 2021-01-05
author: "xiaonan"
math:
 enable: true

tags: [algorithm]
categories: [数据结构]
---

## 选择排序

![](https://img.fengqigang.cn//img/selectionSort.gif)

## C语言实现

```c
#include <stdio.h>

void swap(int *a, int *b)
void selection_sort(int arr[], int len)

void selection_sort(int arr[], int len)
{
	int i, j;
	for(i=0; i<len -1; i++)
	{
		int min = i;
		for(j = i+1; j < len; j++)
			if (arr[j] < arr[min])
				min = j;
		swap(&arr[min], &arr[i]);
	}
}
```
{{< admonition note >}}
1. 前面的元素与后面的元素一一对比, 若后面的元素小，将最小元素的的序号替换成它, 最后前的元素的值与最小序号所对的值替换

2. 即只需要选择n-1个前元素即可（0 -> len - 2），同时需要与后面的所有元素对比(0 -> len - 1)

3. 一次循环结束后确定了最小元素才互换，不是一得到一个较小的元素就互换
{{< /admonition >}}
