---
title: "Bubble_Sort"
date: 2021-01-04T20:48:16+08:00
lastmod: 2021-01-04
author: "xiaonan"
math:
 enable: true

tags: [algorithm]
categories: [数据结构]
---

## 冒泡排序
![](https://www.runoob.com/wp-content/uploads/2019/03/bubbleSort.gif)

<!--more-->

## C语言实现

```C
#include <stdio.h>

void print_list(int arr[], int len);
void bubble_sort(int arr[], int len);

void bubble_sort(int arr[], int len)
	{
	int i, j, temp;
	printf("初始list为:");
	print_list(arr, len);
	printf("\n");
	int k = 1;
	for(i = 0; i < len - 1; i++)
		for (j = 0; j < len - 1 - i; j++)
			if (arr[j] > arr[j + 1]){
				temp = arr[j];
				arr[j] = arr[j+1];
				arr[j + 1] = temp;
				printf("第%d次替换后的list : ", k);
				print_list(arr, len);
				printf("\n");
				k+=1;
			}
}

void print_list(int arr[], int len)
{
	int i;
	for (i=0; i< len; i++)
		printf("%d ", arr[i]);
}

int main() {
	int arr[] = { 22, 34, 3, 4};
	int len = (int) sizeof(arr) / sizeof(*arr);
	bubble_sort(arr, len);

	return 0;
}
```

| 次数 | list 状态 | 解释                                                                                    | i | j | 是否有移动 |
|:----:|-----------|-----------------------------------------------------------------------------------------|:-:|:-:|:----------:|
|   0  | 22 34 3 4 | 初始化                                                                                  | 0 | 0 |            |
|   1  | 22 34 3 4 | 22(前)与34(后)比较, 22小, 不移动, j+1                                                   | 0 | 0->1 |            |
|   2  | 22 3 34 4 | 34(前)与3(后)比较, 3小, 移至前面, j+1                                                   | 0 | 1->2 |      *     |
|   3  | 22 3 4 34 | 34(前)与4(后)比较, 4小, 移至前面，j+1(此时j+1后=len - 1 - i), 跳出当前循环，i+1, j变为0 | 0->1 | 2->3->0 |      *     |
|   4  | 3 22 4 34 | 22(前)与3(后)比较，3小, 移至前面，j+1                                                   | 1 | 0->1 |      *     |
|   5  | 3 4 22 34 | 22(前)与4(后)比较，4小, 移至前面，j+1(此时j+1后=len - 1 - i), 跳出当前循环, i+1, j变为0 | 1->2 | 1->2->0 |      *     |
|   6  | 3 4 22 34 | 3(前)与4(后), 3小，不移动, j+1, (此时j+1=len - 1 - i), 跳出当前循环， i+1 (此时i=len -1)退出上层循环 | 2->3 | 0->1 |            |

![](https://img.fengqigang.cn//img/20210104212148.png)

## 标准冒泡排序时间复杂度与空间复杂度分析

### 时间复杂度

```C
void bubble_sort(int arr[], int len)
{
	int i, j, temp;
	for(i = 0; i < len - 1; i++)
		for (j = 0; j < len -1 -i; j++)
			if (arr[j] > arr[j + 1])
			{
			temp = arr[j];
			arr[j] = arr[j+1];
			arr[j + 1] = temp;
			}
}
```


| 语句                | cost | times                                                              |
|---------------------|------|--------------------------------------------------------------------|
| int i, j, temp      | $C_1$   | 1                                                                  |
| i < len - 1         | $C_2$   | n(n次判断)                                                         |
| i++                 | $C_3$   | n - 1(不满足条件不加)                                              |
| j=0                 | $C_4$   | i++只会执行n-1次，即j=0执行n-1次                                   |
| j < len - 1 - i     | $C_5$   | $t_1$(i=0) + $t_1$(i=1) + ... + $t_1$(i = n-2) + $t_1$(i = n-1), 最多执行n-1次 |
| j++                 | $C_6$   | $t_2$(i=0) + $t_2$(i=1) + ... + $t_2$(i = n-2) + $t_2$(i = n-1)                |
| arr[j + 1] < arr[j] | $C_7$   | $t_3$(i=0) + $t_3$(i=1) + ... + $t_3$(i = n-2) + $t_3$(i = n-1)                |
| swap(arr, j, j+1)   | $C_8$   | $t_4$(i=0) + $t_4$(i=1) + ... + $t_4$(i = n-2) + $t_4$(i = n-1)                |

算法总的运行时间是第一条语句执行时间之和。如果执行一条语句需要c_i步，又共执行了n次这条语句。那么它在运行时间中占cin为计算总运行时间T[n], 对第一对cost与times这积求和。

T(n) = C1 + C2n + C3(n - 1) + C4(n - 1) + C5[t1(i=0) + t1(i=1) + ... + t1(i=n-2)] + c6[t2(i=0) + t2(i=1) + ... t2(i=n-2)] + c7[t3(i=0) + t3(i=1) + ... + t3(i=n-2)] + c8[t4(i=0) + t4(i=1) + ... + t4(i=n-2)]]



#### 最优时间复杂度

第8步，不执行

T(n) = C1 + C2n + C3(n - 1) + C4(n - 1) + C5[t1(i=0) + t1(i=1) + ... + t1(i=n-1)] + c6[t2(i=0) + t2(i=1) + ... t2(i=n-1)] + c7[t3(i=0) + t3(i=1) + ... + t3(i=n-1)]

即可T(n) = O(n^2)

#### 最坏时间复杂度

第8步，均执行

T(n) = C1 + C2n + C3(n - 1) + C4(n - 1) + C5[t1(i=0) + t1(i=1) + ... + t1(i=n-2)] + c6[t2(i=0) + t2(i=1) + ... t2(i=n-2)] + c7[t3(i=0) + t3(i=1) + ... + t3(i=n-2)] + c8[t4(i=0) + t4(i=1) + ... + t4(i=n-2)]]

即可T(n) = O(n^2)

## 冒泡排序优化

1. 在内部循环的时候，一次交换都没有发生时，直接退出循环即可

```c
void bubble_sort(int arr[], int len)
{
	int i, j, temp;
	int flag = 0;
	for(i = 0; i < len - 1; i++){
		for (j = 0; j < len - 1 - i; j++)
			if (arr[j] > arr[j + 1]){
				temp = arr[j];
				arr[j] = arr[j+1];
				arr[j + 1] = temp;
				flag = 1;
			}
	if(flag == 0)
		return;
	}
}
```

此时最优时间复杂度 T(n) = O(n), 外部只执行1次， 内部执行

T(n) = C1 + C2 + C3 + C4(n - 1) + C5(n - 1) + c6(n - 1)



## 参考

1. [Bubble Sort](https://www.geeksforgeeks.org/bubble-sort/)
2. [冒泡排序](https://www.runoob.com/w3cnote/bubble-sort.html)
