---
layout: post
category: solution
title: "leetcode 404 Sum Of Left Leaves"
tags: leetcode
---

# leetcode 404 Sum Of Left Leaves

* 计算所有左叶节点的val的和

## 解法一
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def sumOfLeftLeaves(self, root, left=False):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root:
            return 0
        
        ans = 0
        if left and root.left == None and root.right == None:
            ans += root.val
        
        return ans + self.sumOfLeftLeaves(root.left, True) + self.sumOfLeftLeaves(root.right, False)
```

## note
* 判断左叶子
    * 在上一层节点的左子树中，没有任何子节点
* 根节点不是左子树，如果只有根节点不能计算到和中
