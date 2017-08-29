---
layout: post
category: solution
title: "leetcode 538 Convert BST To Greater Tree"
tags: leetcode
---

# leetcode 538 Convert BST To Greater Tree

* 将二叉查找树变为Greater Tree
* Greater Tree：右子树优先遍历树，根节点值为val加上之前所有遍历过的点之和

## 解法一
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def __init__(self):
        self.sum = 0
        
    def convertBST(self, root):
        """
        :type root: TreeNode
        :rtype: TreeNode
        """
        if root:
            self.convertBST(root.right)
            root.val += self.sum
            self.sum = root.val
            self.convertBST(root.left)
            
        return root
```

## note

* 理解题意中的Greater Tree定义
