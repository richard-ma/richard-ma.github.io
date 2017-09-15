---
layout: post
category: solution
title: "leetcode 26 Remove Duplicates From Sorted Array"
tags: leetcode
---

# leetcode 26 Remove Duplicates From Sorted Array

* 删除一个排序数组的重复元素

## 解法一
```
class Solution(object):
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0
        
        l = 1
        p = 0
        for idx in range(1, len(nums)):
            if nums[idx] != nums[p]:
                l += 1
                p += 1
                nums[p] = nums[idx]
                
        return l
```

## note

* p指针指向最后一个重复的元素
* 当p和idx指向的元素不同时，将idx指向的元素赋值给p对应的元素
