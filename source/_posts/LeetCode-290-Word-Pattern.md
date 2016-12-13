---
title: '[LeetCode]290. Word Pattern'
date: 2016-12-12 16:48:27
categories: "Algorithms"
tags:
- 学习
---
### 问题描述 ###
给定一个模式pattern和一个字符串str，判断str是否满足相同的pattern。
例如：
pattern = "abba", str = "dog cat cat dog" 则返回 true.
<!-- more -->

### 解题思路 ###

### 具体代码 ###
**python**
```python
class Solution(object):
    def wordPattern(self, pattern, str):
        p = pattern
        s = str.split()
        return map(p.find,p) == map(s.index,s)

```
**Java**
```java
public class Solution {
    public boolean wordPattern(String pattern, String str) {
        String[] words = str.split(" ");
        if(pattern.length() != words.length) return false;
        Set<String> set = new HashSet<String>();
        Map<Character,String> map = new HashMap<Character,String>();
        for(int i=0;i<words.length;i++){
            char p = pattern.charAt(i);
            if (map.containsKey(p)){
                if(!map.get(p).equals(words[i])) return false;
            }else {
                if (set.contains(words[i])) return false;
                map.put(p,words[i]);
                set.add(words[i]);
            }
        }
        return true;
    }
}
```
