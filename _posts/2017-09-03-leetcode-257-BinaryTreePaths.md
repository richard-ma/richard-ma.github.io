---
layout: post
category: solution
title: "leetcode 257 Binary Tree Paths"
tags: leetcode
---

# leetcode 257 Binary Tree Paths

* 输出所有的根节点到叶节点的路径

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
        self.ans = []
        
    def binaryTreePaths(self, root, s=""):
        """
        :type root: TreeNode
        :rtype: List[str]
        """
        if root == None:
            return self.ans
        
        if s == "":
            s += str(root.val)
        else:
            s += "->" + str(root.val)
            
        if root.left == None and root.right == None:
            self.ans.append(s)
        
        self.binaryTreePaths(root.left, s)
        self.binaryTreePaths(root.right, s)

        return self.ans
```

## note

* 当左右子树都为空时才是叶节点,才能添加到ans中
* 如果根节点为None,则直接return,否则后面代码会执行
