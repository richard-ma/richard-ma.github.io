---
layout: post
category: solution
title: "leetcode 637 Average Of Levels In Binary Tree"
tags: leetcode
---

# leetcode 637 Average Of Levels In Binary Tree

* 节点按层分组，求每层节点val的平均值

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
        self.data = []
        
    def averageOfLevels(self, root):
        """
        :type root: TreeNode
        :rtype: List[float]
        """
        self.flat(root, 1)
        ans = map(lambda x: sum(x)/float(len(x)), self.data)
        return ans
        
    def flat(self, root, level):
        if len(self.data) < level:
            self.data.append([])
        
        self.data[level-1].append(root.val)
        if root.left != None:
            self.flat(root.left, level+1)
        if root.right != None:
            self.flat(root.right, level+1)
```

## note
* 将树形按层扁平化存储[[3], [9, 20], [15, 7]]
* 使用sum(x) / len(x)求平均数，由于平均数有可能是小数，所以要强制类型转换成float
