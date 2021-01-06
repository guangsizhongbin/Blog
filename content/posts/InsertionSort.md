---
title: "InsertionSort"
date: 2021-01-06T16:31:09+08:00
lastmod: 2021-01-06
author: "xiaonan"
math:
 enable: true

tags: [algorithm]
categories: [数据结构]
---

## 插入排序


![](https://img.fengqigang.cn//img/insertionSort.gif)

## 插入排序的特征

1.从第二个元素(比较元素)开始一一与前面元素(被比较元素)比较, 若当前元素小于被比较元素，被比较元素后移，直到比较元素比被比较元素大或等于时，比较元素插入到被比较元素的位置

 > 比较元素位置:

 从第二个元素到最后一个(n-1个)

 > 被比较元素位置:

 从第一个到比较元素位置-1, 考虑从比较元素位置依次递减，满足>=0即可. 即用`while`

2. 这里一直用的`arr[j+1] = arr[j]`, 采取前面元素覆盖后面元素的方式，当满足条件时，`arr[j+1]`才等于`key`

## C语言实现

```c
#include<stdio.h>

void insertion_sort(int arr[], int len);
void print_list(int arr[], int len);

void insertion_sort(int arr[], int len)
{
	int i, j, key;
	int k=1;
	for(i=1; i<len; i++)
	{
		key = arr[i];
		j=i-1;
		while((j>=0) && (arr[j]>key)){
			arr[j+1] = arr[j];
				j--;
		}
		arr[j+1] = key;
		printf("第%d次list:", k);
		print_list(arr, len);
		printf("\n");
		k+=1;
	}
}

void print_list(int arr[], int len)
{
	int i;
	for(i=0; i<len; i++)
		printf("%d ", arr[i]);
}

int main(void)
{
	int arr[] = {22, 34, 321, 32, 1, 5, 23};
	int len = (int) sizeof(arr) / sizeof(*arr);
	printf("初始list:");
	print_list(arr, len);
	printf("\n");
	insertion_sort(arr, len);
	printf("最终list:");
	print_list(arr, len);


	return 0;
}
```

![](https://img.fengqigang.cn//img/20210106163530.png)

## 复杂度分析

### 时间复杂度

#### 最坏时间复杂度

在数组完全逆序的情况下:

> 插入第2个元素时，考虑对比1个元素 \
> 插入第3个元素时，考虑对比2个元素 \
> 插入第n个元素时，考虑对比n-1个元素

最坏情况下的比较次数是:$1+2+...+n-1=\frac{(n-1)n}{2}$

所以其时间复杂度是: $O(n^2)$



#### 最优时间复杂度

在数组完全正序的情况下:

> 插入第2个元素时，考虑对比1个元素 \
> 插入第3个元素时，考虑对比1个元素 \
> 插入第n个元素时，考虑对比1个元素

最好情况下的比较次数是: $1+1+...+1=n$

所以其时间复杂度是: $O(n)$



### 空间复杂度

{{< admonition note >}}
一个程序在执行时除需要存储空间来存放本身的指令、常数、变量和输入数据外，还需要一些对数据进行操作的工作单元和存储一些为实现计算所需信息的辅助空间。

`算法原地工作`: 是指算法所需的辅助空间为常量, 即$O(1)$
{{< /admonition >}}

此插入排序算法的辅助空间为常量，即其空间复杂度为$O(1)$

## 参考文章

[插入排序 | 菜鸟教程](https://www.runoob.com/w3cnote/insertion-sort.html)
