---
title: "RemoveElement"
date: 2021-03-27T22:21:14+08:00
lastmod: 2021-03-27
author: "xiaonan"
math:
 enable: true

tags: [array]
categories: [leetcode]
---

### 27. Remove Element

#### 双指针法

1. 考虑 nums[x] != val 时, 加入到当前数组中

```java
class Solution {
    public int removeElement(int[] nums, int val) {
			int i = 0;
			for (int x = 0; x < nums.length; x++){
				if (nums[x] != val){
					nums[i] = nums[x];
					i +=1;
				}
			}
			return i;
    }
}
```

---

**优化**

1. 
```java
nums[i] = nums[x];
i += 1;
```

可以直接写成
```java
nums[i++] = nums[x];
```

**疑问**

1. 空数组 与 只声明未赋值的数组 其长度是多少?


---

2. 考虑 nums[x] = val 时, 通过将最后的元素覆盖掉 nums[x] 的值

```
class Solution {
    public int removeElement(int[] nums, int val) {
			
        int i = 0;
				int n = nums.length;

				while(i < n){
					if (nums[i] == val){
						nums[i] = nums[n - 1];
						n--;
					} else {
						i++;
					}
				}
				return n;
    }
}
```

**优化**

1. else 后之有一条语句， 可以去掉

2. 考虑 **nums**


