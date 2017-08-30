---
layout: post
category: solution
title: "leetcode 108 Convert Sorted Tree To BST"
tags: leetcode
---

# leetcode 108 Convert Sorted Tree To BST

* 将一个排好序的数组变为二叉搜索树

## 解法一
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def sortedArrayToBST(self, nums):
        """
        :type nums: List[int]
        :rtype: TreeNode
        """
        if not nums:
            return nums
        
        mid = len(nums) / 2
        root = TreeNode(nums[mid])
        left, right = (nums[:mid], nums[mid+1:])
        root.left = self.sortedArrayToBST(left) if left else None
        root.right = self.sortedArrayToBST(right) if right else None
        
        return root
```

## note
* 取中间元素作为根，创建节点
* 前半部分为左子树，后半部分为右子树
* 当数组为空时，结束递归
* nums初始为空的情况
