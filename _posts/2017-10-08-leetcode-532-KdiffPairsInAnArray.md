---
layout: post
category: solution
title: "leetcode 532 K-diff Pairs In An Array"
tags: leetcode
---

# leetcode 532 K-diff Pairs In An Array

* 找出数组中差为k的不重复的数对个数

## 解法一
```
class Solution(object):
    def findPairs(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        if k > 0:
            return len(set(nums) & set([n+k for n in nums])) # item+k有多少元素在nums集合中,求交集的个数就是数对的数量
        if k == 0:
            return sum(v > 1 for v in collections.Counter(nums).values()) # 出现次数大于1的元素个数,重复过的元素就是数对的数量
        else:
            return 0
```

## note

* 数对题目不要穷举,那样至少是n^2的复杂度
* k是两数差的绝对值,所以不可能出现负数,else分支也可以去掉
