---
layout: post
category: solution
title: "leetcode 653 Two Sum IV"
tags: leetcode
---

# leetcode 653 Two Sum IV

* 找出树形结构中是否存在两个数字的和是给定的数字k

## 解法一
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def findTarget(self, root, k):
        """
        :type root: TreeNode
        :type k: int
        :rtype: bool
        """
        if not root:
            return False
        
        bfs, s = [root], set()
        for i in bfs:
            if k - i.val in s: return True
            s.add(i.val)
            if i.left: bfs.append(i.left)
            if i.right: bfs.append(i.right)
        return False
```

## note
* 使用list做bfs的结点队列
* set可保证不重复元素
