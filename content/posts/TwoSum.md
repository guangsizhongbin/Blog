---
title: "TwoSum"
date: 2021-03-26T22:48:16+08:00
lastmod: 2021-03-26
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [algorithm]
---

[Two Sum 001](https://leetcode.com/problems/two-sum/submissions/)

### 我的代码(双指针法)

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
            if (nums.length < 2){
                return new int[0];
            }
                
			int[] data = new int[2];

			for (int x = 0 ; x < nums.length; x ++){
				for (int y = x + 1; y < nums.length; y ++){
						if (nums[x] + nums[y] == target){
								data[0] = x;
                data[1] = y;
						}
				}
			}
                return data;
    }
}
```

### 最优解(hash表)

待学hash表
