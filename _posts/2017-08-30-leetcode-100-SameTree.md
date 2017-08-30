---
layout: post
category: solution
title: "leetcode 100 Same Tree"
tags: leetcode
---

# leetcode 100 Same Tree

* 判断两棵树是否完全相同
    * 结点值相同
    * 树的结构相同

## 解法一
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def isSameTree(self, p, q):
        """
        :type p: TreeNode
        :type q: TreeNode
        :rtype: bool
        """
        if p and q:
            return p.val == q.val and self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
        else:
            return p == q
```

## note
* 递归算法
* 判断结点值是否相同
* 判断左子树和右子树
* 如果结点均为None，应该判断为相同
