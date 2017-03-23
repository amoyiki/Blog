---
title: '[CareerCup] 1.4 Replace Spaces'
date: 2017-03-20 18:22:17
categories: "Algorithms"
tags:
- 学习
---
### 问题描述 ###
将字符串中的空格替换成“%20”
<!-- more -->
### 解题思路 ###
Java和Python都有相对应的replace方法。但是这么做就没必要写这个题目了。另外如果新建空间来构造也是同样的道理。最科学的方法是in place去改变字符串。
思路是，先遍历一遍字符串，算出有多少个空格，然后resize字符串的长度。接下来从后往前遍历，遇到空格就替换成"%20"

### 具体代码 ###
普通方法:
```python
class Solution:
    def replaceSpace(self,s):
        return s.replace(' ','%20')

```
正经方法：
```java
public class Solution {
    public String replaceSpace(StringBuffer str) {
        int count = 0;
        for(int i=0;i<str.length();i++){
            if(str.charAt(i)==' ')
                count++;
            }
            int oldindex = str.length()-1;
            int newlength = str.length() + count*2;
            int newindex = newlength-1;
            str.setLength(newlength);
            for(;oldindex>=0 && oldindex<newlength;--oldindex){
                if(str.charAt(oldindex) == ' '){
                    str.setCharAt(newindex--, '0');
                    str.setCharAt(newindex--, '2');
                    str.setCharAt(newindex--, '%');
                    }else{
                        str.setCharAt(newindex--, str.charAt(oldindex));
                    }
            }
        return str.toString();
    }
}
```
