---
title: '[LeetCode]217. Contains Duplicate'
date: 2016-11-10 14:44:59
categories: "Algorithms"
tags:
- 学习
---
### 问题描述 ###
给定一个整数数组，判断是否包含重复元素，是返回true。
若都是唯一返回false
<!-- more -->

### 解题思路 ###
利用set这种数据结构的特点，只要set后的数据长度不等于原来的数据长度的话，就证明有重复元素，否则证明没有重复元素。
### 具体代码 ###
**python**
```python
class Solution(object):
    def containsDuplicate(self, nums):
        return len(nums) != len(set(nums))
```

**Java**
```java
public class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set s = new HashSet();
        for(int n:nums){
            s.add(n);
        }
        if(nums.length != s.size()) return true;
        return false;
    }
}
```
