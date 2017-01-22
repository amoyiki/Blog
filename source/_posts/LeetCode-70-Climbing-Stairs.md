---
title: '[LeetCode]70. Climbing Stairs'
date: 2017-01-20 17:28:22
categories: "Algorithms"
tags:
- 学习
---
### 问题描述 ###
有n步楼梯，需要n步才能到顶。每次你可以选择爬1步或2步，需要多少步你才能爬到顶。
<!-- more -->

### 解题思路 ###
这个题目跟斐波那契数列一样。爬到最后一步有两种方式：
- f(n-1) 爬一步到顶
- f(n-2) 爬两步到顶
同时爬1步只有一种方式，爬两步有两种方式。
### 具体代码 ###
**python**
```python
class Solution(object):
    def climbStairs(self,n):
        a,b = 1,1
        for i in range(n):
            a,b = b,a+b
        return a
```
**java**
```java
public class Solution{
    public int climbStairs(int n){
        if(n==0) return 0;
        int a=1,b=1;
        for(int i=0;i<n;i++){
            int temp = a;
            a = b;
            b = a+temp;
        }
        return a;
    }
}

```
