---
title: '[LeetCode]105.Construct Binary Tree from Preorder and Inorder Traversal'
date: 2017-01-05 17:52:05
categories: "Algorithms"
tags:
- 学习
---
### 问题描述 ###
给定树的前序遍历和中序遍历，构建出这个二叉树
<!-- more -->

### 解题思路 ###

### 具体代码 ###
**python**
```python
class Solution(object):
    def buildTree(self, preorder, inorder):
        if not preorder or not inorder:
            return None

        rootValue = preorder.pop(0)
        root = TreeNode(rootValue)
        inorderIndex = inorder.index(rootValue)

        root.left = self.buildTree(preorder, inorder[:inorderIndex])
        root.right = self.buildTree(preorder, inorder[inorderIndex+1:])

        return root
```

**Java**
```java

```
