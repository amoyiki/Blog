---
title: '[LeetCode]153.Find Minimum in Rotated Sorted Array'
date: 2017-01-19 17:45:10
categories: "Algorithms"
tags:
- 学习
---
### 问题描述 ###
一个顺序数组，经过一次旋转
{1,2,3,4,5}  ---> {3,4,5,1,2}
找出最小元素。
<!-- more -->
### 解题思路 ###
无论Java还是Python，只要排序过后就可以找出最小元素。时间复杂度O(n)
如Python方法min()就能直接得出数组最小值。Java也有Arrays.sort()方法排序。
但是如果单纯O(n)的复杂度，明显没有多大的意义。所有这道题应该用二分查找方法来返回最小值。

### 具体代码 ###
**python**
```python
class Solution(object):
    def findMin(self,nums):
        left,right = 0, len(nums) - 1
        while left < right:
            mid = (left + right) / 2
            if nums[mid] <= nums[right]:
                right = mid
            else:
                low = mid + 1
        return nums[low]
```
