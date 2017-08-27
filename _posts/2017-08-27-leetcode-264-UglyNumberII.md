---
layout: post
category: solution
title: "leetcode 264 Ugly Number II"
tags: leetcode
---

# leetcode 264 Ugly Number II

* 当一个数字只有2,3,5三个数字的约数时,称为Ugly Number
* 给一个数字n,求出第n个Ugly Number是多少,n不会超过1640
* 1规定为Ugly Number

## 解法一 TLE
```
class Solution(object):
    def nthUglyNumber(self, n):
    """
    :type n: int
    :rtype: int
    """
    arr = [False, True, True, True, True, True]
                                   
    if n < 6:
        return n
                                                
    n -= 5
    p = 6
    while (1):
        if p % 2 == 0:
            arr.append(arr[p / 2])
        elif p % 3 == 0:
            arr.append(arr[p / 3])
        elif p % 5 == 0:
            arr.append(arr[p / 5])
        else:
            arr.append(False)

        if arr[p] == True:
            n -= 1

        if n == 0: 
            return p

        p += 1
```

## note
* 查表
* 当一个数字x有2这个约数时,它是否为Ugly Number的判定就是看x / 2是否为Ugly Number, 3,5同理
* 这个算法在312个数字查询时超时,因为数字越大Ugly Number出现的概率越小,所以造成超时

## 解法二
```
class Solution(object):
    def nthUglyNumber(self, n):
    """
    :type n: int
    :rtype: int
    """
    ugly = [1]
    i2, i3, i5 = 0, 0, 0
    while n > 1:
        u2, u3, u5 = 2 * ugly[i2], 3 * ugly[i3], 5 * ugly[i5] # 不断构造新数字
        umin = min((u2, u3, u5)) # 选择构造出来最小的数字
        if umin == u2:
            i2 += 1
        if umin == u3:
            i3 += 1
        if umin == u5:
            i5 += 1
        ugly.append(umin)
        n -= 1
    return ugly[-1]
```

## note
* 构造法
* 利用2, 3, 5三个数字,逐步构造出Ugly Number,需要几个就构造到第几个即可
* 这样可以跳过所有非Ugly Number的构造或判断,提升效率
