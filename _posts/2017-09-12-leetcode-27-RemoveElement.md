---
layout: post
category: solution
title: "leetcode 27 Remove Element"
tags: leetcode
---

# leetcode 27 Remove Element

* 将数组中特定数据删除

## 解法一
```
class Solution(object):
    def removeElement(self, nums, val):
        """
        :type nums: List[int]
        :type val: int
        :rtype: int
        """
        if not nums:
            return 0
        
        l = 0
        p = 0
        for k, v in enumerate(nums):
            if val != v:
                if k != p:
                    nums[p] = nums[k]
                l += 1
                p += 1
        
        return l
```

## note

* 指针p指向最后一个被删除的数据位置，用后面的数据覆盖它
* l表示数组长度，超过l的部分被忽略
