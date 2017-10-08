---
layout: post
category: solution
title: "leetcode 414 Third Maximum Number"
tags: leetcode
---

# leetcode 414 Third Maximum Number

* 找出数组中第三大的数
* 如果数字不足三个,返回最大的数

## 解法一
```
class Solution(object):
    def thirdMax(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        
        v = [float('-inf'), float('-inf'), float('-inf')]
        for n in nums:
            if n not in v:
                if n > v[0]: v = [n, v[0], v[1]]
                elif n > v[1]: v = [v[0], n, v[1]]
                elif n > v[2]: v = [v[0], v[1], n]
        
        return max(nums) if float('-inf') in v else v[2]
```

## note

* float('-inf')是最小浮点数的写法
* 元素不在前三大中才计算
