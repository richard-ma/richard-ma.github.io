---
layout: post
category: solution
title: "leetcode 605 Can Place Flowers"
tags: leetcode
---

# leetcode 605 Can Place Flowers

* 只有两侧都是空地才可以种花,给出地是否种花的情况和需要栽种花的数量,测试是否可行

## 解法一
```
class Solution(object):
    def canPlaceFlowers(self, flowerbed, n):
        """
        :type flowerbed: List[int]
        :type n: int
        :rtype: bool
        """
        ans = 0
        
        for i in range(len(flowerbed)):
            if (flowerbed[i] == 0) and (i == 0 or flowerbed[i-1] == 0) and (i == len(flowerbed)-1 or flowerbed[i+1] == 0):
                flowerbed[i] = 1 # set flower
                ans += 1
            
            if ans >= n:
                return True

        return False
```

## note

* 如果地被选中可以种花,则更新值为1
* 如果种花已经超过n则可以终止测试,结论为有可行方案
