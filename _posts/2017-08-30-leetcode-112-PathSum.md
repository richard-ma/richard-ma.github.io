---
layout: post
category: solution
title: "leetcode 112 Path Sum"
tags: leetcode
---

# leetcode 112 Path Sum

* 给出一个数,看是否存在从根到叶的一条路径上所有节点值的和与它相等

## 解法一
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def hasPathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: bool
        """
        if not root:
            return False
        
        if sum == root.val and not root.left and not root.right:
            return True
        else:
            return self.hasPathSum(root.left, sum-root.val) or self.hasPathSum(root.right, sum-root.val)
```

## note
* 当到达叶节点时,检测sum是否已经为0,如果是,则这条路径就是所要的
* 如果到达节点sum不为0,则检测其左右子树是否有路径节点值的和为sum-root.val的值出现
