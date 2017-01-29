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

Climbing Stairs 这题还有一个变种题。题目如下
>一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

代码
### 递归 ###
```python
class Solution:
    def jumpFloorII(self, number):
        if number <=0: return -1
        if number == 1: return 1
        return 2 * self.jumpFloorII(number-1)

```
### 非递归 ###
```python
class Solution:
    def jumpFloorII(self, number):
        # write code here
        if number <= 0: return -1
        if number == 1: return 1
        a = 2
        for i in range(2,number):
            a *=2
        return a
```

还有一道斐波那契数列的变种，题目如下
> 用2*1的小矩形横、竖去覆盖更大的矩形。用n个2*1的小矩形无重叠的覆盖一个2*n的大矩形。共有多少种方法。
> 如果因为是覆盖一个2*n的矩阵，所以当一个2*1的小矩阵竖放时，大矩形的长度就会变成n-1，剩下的需要覆盖的面积就是2*(n-1)
> 如果是横放的话剩下需要覆盖的面积是2*(n-2) ,由此推出f(n) = f(n-1) + f(n-2)
### 非递归 ###
```python
class Solution:
    def rectCover(self, number):
    if number <= 0:
        return 0
    t = [1,2]
    if number <= 2:
        return t[number-1]
    for i in range(2,number):
        t.append(t[i-1]+t[i-2])
    return t[-1]
```

### 递归 ###
```java
public class Solution{
    public int RectCover(int target){
        if(target<=0){
            return 0;
        }else if(target==1){
            return 1;
        }else if(target==2){
            return 2;
        }
        return RectCover(target-1)+RectCover(target-2);
    }
}
```
