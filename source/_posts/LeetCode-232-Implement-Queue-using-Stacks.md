---
title: '[LeetCode]232. Implement Queue using Stacks'
date: 2017-01-11 11:28:14
categories: "Algorithms"
tags:
- 学习
---
### 问题描述 ###
利用堆栈实现队列功能
<!-- more -->

### 解题思路 ###
`Stack`的特点是先进后出，`Queue`的特点是先进先出。利用两个`Stack`，一个负责输入一个负责输出.
如果输出堆栈为空，将输入堆栈值传给输出堆栈，若两个堆栈都为空，返回空值
`python`中用list模拟堆栈.
### 具体代码 ###
**python**
```python
class Queue(object):
    def __init__(self):
        self.stackA = []
        self.stackB = []
    def push(self, x):
        self.stackA.append(x)
    def pop(self):
        self.peek()
        self.stackB.pop()
    def peek(self):
        if self.stackB:
            return self.stackB[-1]
        elif not self.stackA:
            return None
        else:
            while self.stackA:
                self.stackB.append(self.stackA.pop())
            return self.stackB[-1]
    def empty(self):
        return len(self.stackA)==0 and len(self.stackB)==0
```

**Java**
```java

```
