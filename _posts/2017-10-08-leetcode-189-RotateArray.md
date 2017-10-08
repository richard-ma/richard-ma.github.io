---
layout: post
category: solution
title: "leetcode 189 Rotate Array"
tags: leetcode
---

# leetcode 189 Rotate Array

* 计算数组循环右移k位的结果

## 解法一
```
class Solution(object):
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        k = k % len(nums)
        
        def reverseSublist(lst, start, end):
            lst[start:end] = lst[start:end][::-1]
        
        reverseSublist(nums, 0, len(nums))
        reverseSublist(nums, 0, k)
        reverseSublist(nums, k, len(nums))
```

## note

* 三步反序
    * 0~len(nums)反序
    * 0~k-1反序
    * k~len(nums)反序
* 实现了sublist的in place反序算法
