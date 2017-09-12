---
layout: post
category: solution
title: "leetcode 35 Search Insert Position"
tags: leetcode
---

# leetcode 35 Search Insert Position

* 如果查找数字在数组中，返回其位置
* 如果查找数字不在数组中，返回其排序时应该插入的位置

## 解法一
```
class Solution(object):
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        
        for k, v in enumerate(nums):
            if target == v:
                return k
            elif target < v:
                return k
        
        return len(nums)
```

## note
* 扫描一遍数组O(n)复杂度
* 当遇到相等值时，返回其位置
* 当遇到第一个比查找值大的数字时，证明查找的数字应该在这里插入
* 如果扫描完毕都没有找到合适的位置，证明该查找数字应该放在队尾
