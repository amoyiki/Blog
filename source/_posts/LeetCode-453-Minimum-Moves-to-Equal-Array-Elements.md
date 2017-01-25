---
title: '[LeetCode]453.Minimum Moves to Equal Array Elements'
date: 2016-11-09 16:21:57
categories: "Algorithms"
tags:
- 学习
---
### 问题描述 ###
给定一个长度为n的非空数字数组，每次对n-1个加1。
求所有元素值相等，需要几次操作。
<!-- more -->

### 解题思路 ###
操作次数 = 数组总和 - 数组中最小的数*数组长度

### 具体代码 ###
**python**
```python
class Solution(object):
    def minMoves(self, nums):
        return sum(nums) - min(nums)*len(nums)

```

**java**
```java
public class Solution {
    public int minMoves(int[] nums) {
        int min = nums[0];
        int sum = 0;
        for(int i: nums){
            min = Math.min(min,i);
            sum +=i;
        }
        return sum - min*nums.length;
    }
}
```
