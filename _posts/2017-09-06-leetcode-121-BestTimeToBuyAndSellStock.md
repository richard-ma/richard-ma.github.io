---
layout: post
category: solution
title: "leetcode 121 Best Time To Buy And Sell Stock"
tags: leetcode
---

# leetcode 121 Best Time To Buy And Sell Stock

* 找出获利最多的买入价和卖出价
* 只能买卖一次

## 解法一
```
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if len(prices) == 0:
            return 0
        
        ans = 0
        m = prices[0]
        for i in range(1, len(prices)):
            if prices[i] < m:
                m = prices[i]
            elif prices[i] - m > ans:
                ans = prices[i] - m
                
        return ans
```

## note

* 最小值为0号，如果遇到更小的更新
* 如果当前值不是最小值，则减去最小值计算获利，获利大于记录则更新ans
* 如果采用后续数组最大值减去当前值的O(n^2)算法，超时
