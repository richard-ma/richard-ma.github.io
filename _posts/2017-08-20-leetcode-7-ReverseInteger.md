---
layout: post
category: solution
title: "leetcode 7 Reverse Integer"
tags: leetcode
---

# leetcode 657 Judge Route Circle

* 将数字x以字符串翻转的形式输出
    * 注意如果是负数翻转后也要加上负数
    * 如果数字翻转后超过32位的表示范围输出0
* 模拟题
    * 按步骤做即可,注意特殊的负数和溢出的问题

## 解法一

```
class Solution(object):
    def reverse(self, x):
    """
    :type x: int
    :rtype: int
    """
    negative = False
    if (x < 0):
        negative = True
        x = abs(x)
                                                                                       
    reversed_x = int(''.join(list(reversed(list(str(x))))))
                                                                                                       
    if negative:
        reversed_x *= (-1)
                                                           
    return 0 if reversed_x < (-1) * (2 ** (32-1)-1) or reversed_x > 2 ** (32-1) else reversed_x
```

## note
* 32位有符号整型变量范围是-(2^31-1) ~~ (2^31), 以为最高位是符号位
* reversed函数的返回结果是一个对象,需要用list强制转换成数组

## 解法二
```
def reverse(self, x):
    s = cmp(x, 0)
    r = int(`s*x`[::-1])
    return s*r * (r < 2**31)
```

## note
* cmp是比较数字和0,如果大于0返回1,等于返回0,小于返回-1 [python 3.6中已经移除]
* [::-1]可以快速的对数组进行反序
* 32位有符号整型的数字绝对值都小于2**31
