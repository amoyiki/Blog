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
相对于Python的数组切割,Java取下标值来获取每次递归所需的值区间。所以需要一个辅助函数来负责递归。
前序遍历中第一个元素pre[0]一定是root节点。
假设该节点的元素在中序中是在in[5],那么中序中的in[0] ~ in[4]就是左子树，
in[6] ~ end 就是右子树。
第二次递归，左子树从pre[1]开始(即pre[0]的下移一位)。中序数组从0~4
右子树从pre[0+5-0+1]开始,中序数组从6~end
第三次
...

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
public class Soultion{
    public TreeNode buildTree(int[]preorder, int[] inorder){
        return helper(0,0,inorder.length-1,preorder,inorder);
    }
    public TreeNode helper(int preStart, int inStart, int inEnd, int[] pre,int[] in){
        if(preStart > pre.length - 1 || inStart > inEnd){
            return null;
        }
        TreeNode root = new TreeNode(pre[preStart]);
        int inIndex = 0; // root节点在中序数组中的下标位置
        for(int i == inStart; i<= inEnd; i++){
            if(in[i]==root.val){
                inIndex = i;
            }
        }
        /* 
        左子树：前序数组从当前root下标的下一位开始，中序数组从开头开始到当前root下标的前一位结束
        右子树：前序数组从当前root下标的下一位，中序数组从root下标下一位到结束
        */
        root.left = helper(preStart + 1, inStart, inIndex - 1, pre, in);
        root.right = helper(preStart + inIndex - inStart + 1, inIndex + 1, inEnd , pr, in);
        return root;
    }
}
```
