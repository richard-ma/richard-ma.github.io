---
layout: post
category: solution
title: "leetcode 66 Plus One"
tags: leetcode
---

# leetcode 66 Plus One

* 高精度加法

## 解法一
```
class Solution(object):
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        digits[-1] += 1
        
        for p in range(len(digits)-1, 0, -1):
            if digits[p] > 9:
                digits[p-1] += 1
            digits[p] = digits[p] % 10
        
        if digits[0] > 9:
            digits[0] %= 10
            digits = [1] + digits
        
        return digits
```

## note

* 最高位要单独处理，如999+1
