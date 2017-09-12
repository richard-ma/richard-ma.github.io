---
layout: post
category: solution
title: "leetcode 661 Image Smoother"
tags: leetcode
---

# leetcode 661 Image Smoother

* 取二维数组周边8个数字的平均数作为当前值

## 解法一
```
        from copy import deepcopy as copy
        
        x_len = len(M)
        y_len = len(M[0]) if x_len else 0
        res = copy(M)
        for x in range(x_len):
            for y in range(y_len):
                neighbors = [
                    M[_x][_y]
                    for _x in (x-1, x, x+1)
                    for _y in (y-1, y, y+1)
                    if 0 <= _x < x_len and 0 <= _y < y_len
                ]
                res[x][y] = sum(neighbors) // len(neighbors)
        return res
```

## note

* 下标越界处理
