---
title: Python一些小技巧
date: 2016-10-10 15:31:11
categories: "Python"
tags:
- 学习
---


## 排序 ##
### 列表和字典混合排序 ###
<!-- more -->
```python
persons = [{'name':'zhang3','age':15},{'name':'li4','age':12}]
persons.sort(lambda a,b:a['age']-b['age']) # 按照年龄排序

```
