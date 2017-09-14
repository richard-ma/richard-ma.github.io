---
layout: post
category: solution
title: "leetcode 119 Pascal's Triangle II"
tags: leetcode
---

# leetcode 119 Pascal's Triangle II

* 给出行数，输出杨辉三角对应的行的数据

## 解法一
```
class Solution(object):
    def getRow(self, rowIndex):
        """
        :type rowIndex: int
        :rtype: List[int]
        """
        ans = [1]
        for _ in range(0, rowIndex):
            ans = [x + y for x, y in zip([0]+ans, ans+[0])]
            
        return ans
```

## note

* zip：zip([1, 2], [3, 4]) -> [(1, 2), (3, 4)]
* [0, 1, 2, 1] 和 [1, 2, 1, 0] 对应元素相加迭代出下一行 [1, 3, 3, 1]
