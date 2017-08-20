---
layout: post
category: solution
title: "leetcode 657 Judge Route Circle"
tags: leetcode
---

# leetcode 657 Judge Route Circle

* 给出一个表示移动的字符序列,判断按照这个顺序移动后是否能回到原点,如果可以则显示true,否则显示false
* 根据移动序列判断L和R以及U和D各自是否个数相同,相同则表示能够回到原点,否则不能

## 解法一: 扫描字符串统计四种字符的个数,然后比较个数是否相同

```
class Solution(object):
    def judgeCircle(self, moves):
        """
        :type moves: str
        :rtype: bool
        """
        countL = countR = countD = countU = 0
                                                   
        for step in moves:
            if step == 'L':
                countL += 1
            elif step == 'R':
                countR += 1
            elif step == 'U':
                countU += 1
            elif step == 'D':
                countD += 1
                                                                                                                                                           
        return countL == countR and countU == countD
```

## 解法二: 利用collections.Counter统计四种字符个数

```
def judgeCircle(self, moves):
    c = collections.Counter(moves)
    return c['L'] == c['R'] and c['U'] == c['D']
```
