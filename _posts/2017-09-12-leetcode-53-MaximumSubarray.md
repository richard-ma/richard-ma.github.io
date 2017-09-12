---
layout: post
category: solution
title: "leetcode 53 Maximum Subarray"
tags: leetcode
---

# leetcode 53 Maximum Subarray

* 找出最大和的连续子数组

## 解法一
```
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        ans = s = nums[0]
        for v in nums[1:]:
            if v > s + v:
                s = v
            else:
                s += v
            
            if s > ans:
                ans = s
                
        return ans
```

## note

* 当前值加之前的和与当前值比较，取最大值作为和
* 如果之前的和加上当前值比当前值还小，那么之前的和是负数，应该舍弃，从当前值开始从新计算求和
