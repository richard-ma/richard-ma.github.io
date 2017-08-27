---
layout: post
category: solution
title: "leetcode 263 Ugly Number"
tags: leetcode
---

# leetcode 263 Ugly Number

* 当一个数字只有2,3,5三个数字的约数时,称为Ugly Number
* 给定一个数字,判断其是否为Ugly Number

## 解法一
```
class Solution(object):
    def isUgly(self, num):
    """
    :type num: int
    :rtype: bool
    """
    if num == 0:
        return False
                                                              
    while (1):
        if num % 5 == 0:
            num = num / 5
        elif num % 3 == 0:
            num = num / 3
        elif num % 2 == 0:
            num = num / 2
        else:
            break
    return True if num == 1 else False
```

## note
* 输入有可能为0,0不是Ugly Number
* 将给定的数字不断除以2,3,5,如果最后能为1,则是Ugly Number,否则不是

## 解法一的代码精简版
```
def isUgly(self, num):
    """
    :type num: int
    :rtype: bool
    """
    if num <= 0:
        return False

    for x in [2, 3, 5]:
        while num % x == 0:
            num = num / x

    return num == 1
```
