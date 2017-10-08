---
layout: post
category: solution
title: "leetcode 695 Max Area Of Island"
tags: leetcode
---

# leetcode 695 Max Area Of Island

* 找出二维数组中面积最大岛的面积
* 1表示陆地,0表示海洋

## 解法一
```
class Solution(object):
    def maxAreaOfIsland(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        seen = set()
        
        def area(r, c):
            if not ( 0 <= r < len(grid) and 0 <= c < len(grid[0])
                   and (r, c) not in seen and grid[r][c]):
                return 0
            seen.add((r, c))
            return (1 + area(r+1, c) + area(r-1, c) +
                       area(r, c+1) + area(r, c-1))
        
        return max(area(r, c)
                  for r in range(len(grid))
                  for c in range(len(grid[0])))
```

## note

* 算法类似种子填色
* 穷举所有点作为起始点的可能,找出max值
