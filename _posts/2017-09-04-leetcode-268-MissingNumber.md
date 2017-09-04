---
layout: post
category: solution
title: "leetcode 268 Missing Number"
tags: leetcode
---

# leetcode 268 Missing Number

* 给出数组，找出连续数字中丢失的那个数

## 解法一
```
class Solution(object):
    def missingNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        nums = sorted(nums)
        
        if nums[0] != 0:
            return 0
        if nums[-1] != len(nums):
            return len(nums)
        
        for i in range(1, len(nums)):
            if nums[i] - nums[i-1] > 1:
                return nums[i]-1
```

## note
* 丢失的数字可能是0或n，头和尾是特殊情况
* 数组需要先排序再验证

## 解法二
```
class Solution(object):
    def missingNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        return n * (n+1) / 2 - sum(nums)
```

## note
* 等差数列求和算出0到n连续数字的和，然后减掉实际数组中数字的和，差就是缺少的数字
