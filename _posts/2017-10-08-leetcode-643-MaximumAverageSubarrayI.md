---
layout: post
category: solution
title: "leetcode 643 Maximum Average Subarray I"
tags: leetcode
---

# leetcode 643 Maximum Average Subarray I

* 在数组中找出k个数字的最大平均数

## 解法一 TLE
```
class Solution(object):
    def findMaxAverage(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: float
        """
        ans = sum(nums[:k]) / float(k)
        
        for i in range(len(nums)-k+1):
            ans = max(ans, sum(nums[i:i+k])/float(k))
        
        return ans
```

## 解法二
```
class Solution(object):
    def findMaxAverage(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: float
        """
        ans = s = sum(nums[:k])
        
        for i in range(1, len(nums)-k+1):
            s = s - nums[i-1] + nums[i+k-1]
            ans = max(ans, s)
        
        return ans / float(k)
```

## note

* 找出k个数字最大和 / k
* 直接计算会TLE,如解法一
* 计算和的部分是重复计算,所以可以简化,计算时记录前面数字的和
* 空间换时间
