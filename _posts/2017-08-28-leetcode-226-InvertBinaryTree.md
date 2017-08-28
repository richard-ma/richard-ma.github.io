---
layout: post
category: solution
title: "leetcode 226 Invert Binary Tree"
tags: leetcode
---

# leetcode 226 Invert Binary Tree

* 交换所有节点的左右子树

## 解法一
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def invertTree(self, root):
        """
        :type root: TreeNode
        :rtype: TreeNode
        """
        if root:
            root.left, root.right = (self.invertTree(root.right), self.invertTree(root.left))
            return root
```

## note
* 递归解法
* 交换左右子树的子节点
* 交换本节点的左右子树
* 注意节点为0的情况，所以开始要对root做判断
