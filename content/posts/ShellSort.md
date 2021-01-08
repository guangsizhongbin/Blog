---
title: "ShellSort"
date: 2021-01-07T09:34:11+08:00
lastmod: 2021-01-07
author: "xiaonan"
math:
 enable: true


tags: [algorithm]
categories: [数据结构]
---

## ShellSort

Shell 排序动图

![](https://img.fengqigang.cn//img/Sorting_shellsort_anim.gif)

<!--more-->


{{< admonition tip >}}
> 1. `14>>2` 如何计算？

`>>`为右移运算符

14 的二进制为(0000 1110)

正数向右移动，低位舍弃，高位补零

移动之后的二进制为(0000 0011), 为3

```c
#include <stdio.h>

int main(void)
{
	int number = 14 >> 2;
	printf("右移二位后的值为: %d ", number);
}
```
![](https://img.fengqigang.cn//img/20210107094949.png)

> 2. `gap = len >> 1` 是什么意思？

表示 gap = len 不断的对半分

{{< /admonition >}}

## ShellSort C语言实现

```c
#include <stdio.h>

void print_list(int arr[], int len);
void shell_sort(int arr[], int len)
{
	int gap, i, j;
	int temp;
	int k = 1;
	for (gap = len >> 1; gap > 0; gap >>= 1){
		printf("gap 为%d时: \n", gap);
		for (i = gap; i<len; i++)
		{
			temp = arr[i];
			for(j = i-gap; j>=0 && arr[j] > temp; j -= gap)
				arr[j + gap] = arr[j];
			arr[j + gap] = temp;
			printf("第%d次list: ", k);
			print_list(arr,len);
			k+=1;
			printf("\n");
		}
	}
}

void print_list(int arr[], int len)
{
	for(int i=0;i<len;i++)
		printf("%d ", arr[i]);
}

int main (void)
{
	int arr[] = {3, 21, 412, 1, 4,39, 123, 6};
	int len = (int) sizeof(arr) /sizeof (*arr);

	printf("初始list: ");
	print_list(arr,len);
	printf("\n");

	shell_sort(arr,len);
	printf("最终list: ");
	print_list(arr,len);
	printf("\n");
}
```
gap = 4

![](https://img.fengqigang.cn//img/20210107105627.png)

gap = 2

![](https://img.fengqigang.cn//img/20210107105743.png)

gap = 1

![](https://img.fengqigang.cn//img/20210107105821.png)

## Shell 排序复杂度和稳定性分析

> 1. 啥是序偶(Ordered pair)?

`序`: 就是有序的意思

`偶`: 一对儿

> 2. 证明N个互异的数组的平均逆序数是$N(N-1)/4$

表$L$: 34, 8, 64, 51, 32, 21

其反序表$L_r$: 21, 32, 51, 64, 8, 34

该表中任意两个数的序偶$(x, y)$, 且$y > x$, 显然在$L$与$L_r$中，在表L和它的反序表$L_r$中的序偶的总个数为$C_N^2=N(N-1)/2$, 因此，平均每个表的逆序是$N(N-1)/4$

> 3. 证明通过交换相邻元素进行排序的任何平均需要$\Omega(N^2)$

已知初始的平均逆序数$N(N - 1)/4 = \Omega(N^2)$, 而每次交换只减少一个逆序，因此需要$\Omega(N^2)$交换

### 时间复杂度

> 为啥希尔排序的时间复杂度可以突破$O(N^2)$?

![](https://img.fengqigang.cn//img/20210107212927.png)

![](https://img.fengqigang.cn//img/20210107212950.png)

#### 以希尔增量时希尔排序的最坏情形为$O(N^2)$

> 啥是希尔增量?

希尔排序使用一个序列$h_1, h_2, ... h_t$, 叫做增量序列

`希尔增量`：$h_t = \lfloor N/2 \rfloor$

$h_k = \lfloor h_{k+1} \rfloor$ 相隔 $h_k$个元素都被排序，此时称文件是$h_k$排序



#### 以Hibbard增量的希尔排序的最坏情形为$O( N^\frac{3}{2})$

> 啥是Hibbard增量？

$1, 3, 7, ..., 2^k - 1$

### 空间复杂度

$O(1)$

### 稳定性

{{<  admonition tip >}}
在一个数组中，存在相同的数，经过排序后，这些数的相对次序保持不变，即原来数组中r[i] = r[j], r[i] 在r[j] 之前，经过排序后，r[i]仍在r[j]之前， 则称这种排序算法是稳定的，否则称为不稳定的。
{{<  /admonition >}}

序列：

3 5 10 $8_1$ 7 2 $8_2$ 1 20 6

`对于gap=5时` (3, 2), (5, $8_2$), (10, 1), ($8_1$, 20), (7, 6)

`排序后`(2, 3), (5, $8_2$), (1, 10), ($8_1$, 20), (7, 6)

2 5 1 $8_1$ 7 3 $8_2$ 10 20 6

`对于gap=2时，向下取整` (2, 1, 7, $8_2$, 20), (5, $8_1$, 3, 10, 6)

`排序后` (1, 2, 7, $8_2$, 20), (3, 5, 6, $8_1$, 10)

1, 3, 2, 5, 7, 6, $8_2$, $8_1$, 20, 10

> 此时$8_2$已经跑到$8_1$之前，表示Shell排序不稳定


## 如何用C语言实现Hibbard增量的Shell排序?

> 1. 为什么要从希尔增量变成Hibbard增量？

![](https://img.fengqigang.cn//img/20210107204444.png)

`在希尔增量的情况下:`

间隔为8时，分为8组

(1, 5), (9, 13), (2, 6), (10, 14), (3, 7), (11, 15), (4, 8), (12, 16)

间隔为4时，分为4组

(1, 3, 5, 7), (9, 11, 13, 15), (2, 4, 6, 8), (10, 12, 14, 16)

间隔为2时，分为2组

(1, 2, 3, 4, 5, 6, 7, 8), (9, 10, 11, 12, 13, 14, 15, 16)

间隔为1时，分为1组

(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16)

`前3个增量没有起任何作用`

> 2. 啥是一个好的增量？

- 最后一个增量必须为1

- 避免序列中的值(尤其是相邻的值)互为倍数的情况


## 参考文章

[数据结构与算法——希尔排序](https://www.cnblogs.com/cciejh/p/14161072.html)

[希尔排序增量序列简介](https://blog.csdn.net/Foliciatarier/article/details/53891144)

[希尔排序为什么会那么牛那么快，能够证明吗？](https://www.zhihu.com/question/24637339)
