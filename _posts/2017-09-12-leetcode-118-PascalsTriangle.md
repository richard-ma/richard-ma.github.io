---
layout: post
category: solution
title: "leetcode 118 Pascal Triangle"
tags: leetcode
---

# leetcode 118 Pascal Triangle

* 产生一个杨辉三角数组

## 解法一
```
class Solution(object):
    def generate(self, numRows):
        """
        :type numRows: int
        :rtype: List[List[int]]
        """
        ans = list()
        
        for n in range(1, numRows+1):
            if n == 1:
                ans.append([1])
            elif n == 2:
                ans.append([1,1])
            else:
                line = list()
                line.append(1)
                
                for p in range(1, len(ans[-1])):
                    line.append(ans[-1][p-1] + ans[-1][p])
                
                line.append(1)
                ans.append(line)
                
        return ans
```

## note

* 注意第一行和第二行的边界条件
* 每行首尾要加元素1
* 迭代公式
