---
layout: post
category: solution
title: "leetcode 219 Contains Duplicate II"
tags: leetcode
---

# leetcode 219 Contains Duplicate II

* 在数组中判断是否有相同的两个数,且这两个数距离最大为k

## 解法一
```
class Solution(object):
    def containsNearbyDuplicate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: bool
        """
        dic = dict()
        for i, v in enumerate(nums):
            if v in dic and i - dic[v] <= k:
                return True
            dic[v] = i
        return False
```

## note

* 设置辅助字典存储,key为数组的值,value为该值的最后出现位置
* 从头遍历数组,如果该值字典中没有记录,则存储
* 如果该值出现过,则计算现在和记录位置的差,小于k则返回True
* 直到函数退出没有找到则返回False
