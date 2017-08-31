---
layout: post
category: solution
title: "leetcode 543 Diameter Of Binary Tree"
tags: leetcode
---

# leetcode 543 Diameter Of Binary Tree

* 找出树种距离最远的两个结点的距离

## 解法一
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def diameterOfBinaryTree(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        self.best = 1
        def depth(root):
            if not root: return 0
            left = depth(root.left)
            right = depth(root.right)
            self.best = max(self.best, left+right+1)
            return max(left, right) + 1
        depth(root)
        return self.best-1
```

## note
* 如果左右子树都有，则计算左右子树最远节点的距离，和目前最大的距离比较
* 当前节点最远距离为左右子树最远节点距离的大的值+1
* 如果只有一个子树，则直接将当前到最远节点的距离+1
* 返回最远距离-1作为结果
