---
layout: post
category: solution
title: "leetcode 628 Maximum Product Of Three Numbers"
tags: leetcode
---

# leetcode 628 Maximum Product Of Three Numbers

* 在数组里选择三个数字，使得他们的乘积为最大
* 两个负数相乘积为正数
    * 三个负数的积为负数
    * 尽量不选择0，除非其他乘积都为负
    * 结果为正数的情况有两负一正和三个正

## 解法一：
```
class Solution(object):
    def maximumProduct(self, nums):
    """
    :type nums: List[int]
    :rtype: int
    """
    s = sorted(nums)[::-1]
    if s[2] > 0:
        return s[0]*(max(s[1]*s[2], s[-1]*s[-2]))
    elif s[2] <= 0:
        return s[0]*s[-1]*s[-2]
    elif s[1] <= 0:
        return s[0]*s[-1]*s[-2]
    elif s[0] <= 0:
        return s[0]*s[1]*s[2]
```

## note
* 将nums数组降序排列
* 如果最大三个数字都为正数，则取最大正数的三正组合和一正两负组合的比较大的作为结果
* 如果最大三个数字包含一个正数或两个正数，取一正两负组合为结果
* 如果三个均为负数，则去最大的三个负数为结果

## 优化解法一：
```
class Solution(object):
    def maximumProduct(self, nums):
    """
    :type nums: List[int]
    :rtype: int
    """
    s = sorted(nums, reverse=True)
    if s[2] > 0:
        return s[0]*max(s[1]*s[2], s[-1]*s[-2])
    elif s[0] <= 0:
        return s[0]*s[1]*s[2]
    else:
        return s[0]*s[-1]*s[-2]
```

## note
* [::-1]这中反序效率不如sorted(reverse=True)快
* 合并了两种分支条件
