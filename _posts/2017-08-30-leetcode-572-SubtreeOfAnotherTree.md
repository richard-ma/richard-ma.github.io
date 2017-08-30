---
layout: post
category: solution
title: "leetcode 572 Subtree Of Another Tree"
tags: leetcode
---

# leetcode 572 Subtree Of Another Tree

* 查找s的子树中是否有t

## 解法一
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def isSubtree(self, s, t):
        """
        :type s: TreeNode
        :type t: TreeNode
        :rtype: bool
        """
        
        def _isSameTree(s, t):
            if s and t:
                return s.val == t.val and _isSameTree(s.left, t.left) and _isSameTree(s.right, t.right)
            else:
                return s == t
        
        if s and t:
            if _isSameTree(s, t):
                return True
            else:
                return self.isSubtree(s.left, t) or self.isSubtree(s.right, t)
        else:
            return s == t
```

## note

* s本身也是s的子树
* 处理s和t为空的情况
* 递归检查所有s的子树是否和t相同
