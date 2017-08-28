---
layout: post
category: solution
title: "leetcode 606 Construct String From Binary Tree"
tags: leetcode
---

# leetcode 606 Construct String From Binary Tree

* 根据二叉树构造字符串

## 解法一
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def tree2str(self, t):
        """
        :type t: TreeNode
        :rtype: str
        """
        ans = ''
        if t:
            ans += str(t.val)
            if t.left != None:
                ans += '('+self.tree2str(t.left)+')'
            elif t.left == None and t.right != None:
                ans += '()'
            if t.right != None:
                ans += '('+self.tree2str(t.right)+')'
        return ans
```

## note
* val(left)(right)
    * left == None: val()(right)
    * right == None: val(left)
* 递归解法
* 注意节点为0的情况，所以开始要对root做判断
