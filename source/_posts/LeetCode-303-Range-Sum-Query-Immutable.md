---
title: '[LeetCode]303. Range Sum Query - Immutable'
date: 2016-12-07 14:34:39
categories: "Algorithms"
tags:
- 学习
---
### 问题描述 ###
给定一个数字数组，求下标在i和j(i ≤ j)之间的元素和
<!-- more -->
### 解题思路 ###
利用一个辅助数组sums[x+1]来存储当前位置与之前元素的累加和

### 具体代码 ###
**python**
```python
class NumArray(object):
    def __init__(self,nums):
        size = len(nums)
        # 辅助函数sums，计算每个位置与之前的数字累积和
        self.sums = [0] * (size + 1)
        for x in range(size):
            # 当前(x+1)位置元素累积和 = 前一位(累积和)+当前元素
            self.sums[x + 1] += self.sums[x] + nums[x]

    def sumRange(self,i,j):
        return self.sums[j+1] - self.sums[i]
```

**Java**
```java
public class NumArray {
    public int[] sums;
    public NumArray(int[] nums) {
        int size = nums.length;
        sums = new int[size+1];
        for(int i=0;i<size;i++){
            sums[i+1] = sums[i] + nums[i];
        }
    }

    public int sumRange(int i, int j) {
        return sums[j+1] - sums[i];
    }
}
```
