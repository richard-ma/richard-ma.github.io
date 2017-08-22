---
layout: post
category: solution
title: "leetcode 617 Merge Two Binary Trees"
tags: leetcode
---

# leetcode 617 Merge Two Binary Trees

* 合并两个二叉树
* 对应位置的值相加
* 一棵树有的节点都要加到新树中

## 解法一
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def mergeTrees(self, t1, t2):
    """
    :type t1: TreeNode
    :type t2: TreeNode
    :rtype: TreeNode
    """
    if not t1 and not t2: # t1和t2都是None则返回None
        return None
    ans = TreeNode((t1.val if t1 else 0) + (t2.val if t2 else 0)) # 如果t1和t2有值则使用，否则值为0，再将t1和t2相加
    ans.left = self.mergeTrees(t1 and t1.left, t2 and t2.left) # 处理左子树
    ans.right = self.mergeTrees(t1 and t1.right, t2 and t2.right) # 处理右子树
    return ans
```

## note
* A and B 当A和B都为真时，返回最后一个表达式B；当有假值出现时，返回第一个假值
