---
layout: post
category: solution
title: "leetcode 107 Binary Tree Level Order Traversal II"
tags: leetcode
---

# leetcode 107 Binary Tree Level Order Traversal II

* 按层将二叉树变为数组
* 将每层的数组按从叶到根的顺序排列

## 解法一
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def levelOrderBottom(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        self.ans = list()
        def dfs(root, level = 0):
            if root:
                if len(self.ans) <= level:
                    self.ans.append(list())
                self.ans[level].append(root.val)
                
                if root.left: dfs(root.left, level+1)
                if root.right: dfs(root.right, level+1)
        
        dfs(root)
        return self.ans[::-1]
```

## note

* 用dfs将二叉树变为数组
* 用-1步长将数组逆序
