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

void print_list(int arr[], int len);
void selection_sort(int arr[], int len);
void swap(int *a, int *b);

void selection_sort(int arr[], int len)
{
	int i, j;
	printf("初始list:");
	print_list(arr, len);
	printf("\n");
	int k = 1;
		for(i=0; i<len -1; i++)
		{
			int min = i;
			for(j = i + 1; j < len; j++)
				if (arr[j] < arr[min])
					min = j;
			swap(&arr[min], &arr[i]);
			printf("第%d次交换后的list:", k);
			print_list(arr, len);
			printf("\n");
			k+=1;
		}
}

void swap(int *a, int *b)
{
	int temp = *a;
	*a = *b;
	*b = temp;
}


void print_list(int arr[], int len)
{
	int i;
	for (i=0; i< len; i++)
		printf("%d ", arr[i]);
}

int main() {
	int arr[] = { 22, 34, 3, 4, 5, 9};
	int len = (int) sizeof(arr) / sizeof(*arr);
	selection_sort(arr, len);

	return 0;
}
```
{{< admonition note >}}
1. 前面的元素与后面的元素一一对比, 若后面的元素小，将最小元素的的序号替换成它, 最后前的元素的值与最小序号所对的值替换

2. 即只需要选择n-1个前元素即可（0 -> len - 2），同时需要与后面的所有元素对比(0 -> len - 1)

3. 一次循环结束后确定了最小元素才互换，不是一得到一个较小的元素就互换
{{< /admonition >}}
 
 ## 时间复杂度与空间复杂度分析

 ### 时间复杂度

1. 第一次内循环(1 -> len - 1), N - 1次
2. 第二次内循环(2 -> len - 1), N - 2次
3. 第三次内循环(3 -> len - 1), N - 3次
3. 第后一次内循环(len - 2 -> len - 1), 1次

比较的次数是`(N - 1) + (N - 2) + ... + 1` , 其和是 $\frac{N(N-1)}{2}$

所以其时间复杂度是$O(N^2)$


 ### 空间复杂度

 O(1)

 ## 参考文章

 [选择排序](https://www.runoob.com/w3cnote/selection-sort.html)
