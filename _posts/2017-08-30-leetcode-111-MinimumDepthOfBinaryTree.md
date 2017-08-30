---
layout: post
category: solution
title: "leetcode 111 Minimum Depth Of Binary Tree"
tags: leetcode
---

# leetcode 111 Minimum Depth Of Binary Tree

* 求出二叉树中最短的根节点到叶节点的长度

## 解法一
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def minDepth(self, root, level=1):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root:
            return 0
        elif not root.left and not root.right:
            return level
        elif root.left and root.right:
            return min(self.minDepth(root.left, level+1), self.minDepth(root.right, level+1))
        elif root.left and not root.right:
            return self.minDepth(root.left, level+1)
        elif root.right and not root.left:
            return self.minDepth(root.right, level+1)
```

## note
* 叶节点的定义是左右子树都为None,否则不是叶节点
* 可能有根为None的情况出现,需要单独处理
