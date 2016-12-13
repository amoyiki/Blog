---
title: '[LeetCode]409.Longest Palindrome'
date: 2016-11-09 10:50:21
categories: "Algorithms"
tags:
- 学习
---

### 问题描述 ###
求一串字符串最大的回文子字符串长度
<!-- more -->
**注意：**
1.大小写敏感.
2.默认字符串全大写或全小写

### 解题思路 ###
偶数字符个数累加；奇数字符个数先减一再累加，同时计算奇数个数。
最后如果奇数个数大于0，累加结果再加1。
### 具体代码 ###
**python**
```python
class Solution(object):
    def longestPalindrome(self, s):
        ans = odd = 0
        count = collections.Counter(s)
        for i in count:
            ans += count[i]
            if count[i] % 2 == 1:
                ans -= 1
                odd += 1
        return ans + (odd > 0)
```

**Java**
```java
class Soultion {
    public int longestPalindrome(String s) {
        int len = 0;
        boolean[] map = new boolean[128];
        for(char c : s.toCharArray()){
            map[c] = !map[c];//将有字符的位置由false变成true
            //如果该位置为false的话证明有偶数个数存在
            if(!map[c]) len += 2;
        }
        //如果字符串长度大于已累计长度，添加一个元素放在回文字符串中间
        if (len < s.length())len++;
        return len;
    }
}
```
