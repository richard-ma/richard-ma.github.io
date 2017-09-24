---
layout: post
category: solution
title: "leetcode 88 Merge Sorted Array"
tags: leetcode
---

# leetcode 88 Merge Sorted Array

* 按大小顺序合并两个已排序数组

## 解法一
```
class Solution(object):
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: void Do not return anything, modify nums1 in-place instead.
        """
        p = 0
        for p2 in range(0, n):
            while p < m and nums1[p] <= nums2[p2]:
                p += 1
                
            if p < m:
                nums1.insert(p, nums2[p2])
            else:
                nums1.insert(m, nums2[p2])
            
            m += 1
        
        while len(nums1) > m:
            del nums1[-1]
```

## note

* 数组长度不可以用len识别,要通过读取m和n获得
* 结果的数组要把多余元素删除
