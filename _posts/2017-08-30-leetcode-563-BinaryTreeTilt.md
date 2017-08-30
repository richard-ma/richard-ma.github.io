---
layout: post
category: solution
title: "leetcode 563 Binary Tree Tile"
tags: leetcode
---

# leetcode 563 Binary Tree Tile

* 叶节点tilt为0
* 普通节点tilt为左子树和右子树tilt差的绝对值
* 程序输出所有节点tilt之和

## 解法一
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def findTilt(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root:
            return 0
        
        sum_left = self.findTilt(root.left)
        sum_right = self.findTilt(root.right)
        
        left = root.left.val if root.left else 0
        right = root.right.val if root.right else 0
                
        root.val = root.val + left + right
        
        return abs(left - right) + sum_left + sum_right
```

## note

* 根节点的val为左右子树所有节点val之和
* 先更新根节点val
* 递归计算本节点tilt并返回本节点和本节点子节点的tilt的和
