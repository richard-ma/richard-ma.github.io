---
layout: post
category: bitOperation
title: "[说说位运算] 不用临时变量交换两个数"
tags: bit algorithm
---

# 教科书方法

temp = a
a = b
b = temp

这里是需要一个临时变量temp来起到交换变量的效果。

# 不用临时变量的减法版

a = a - b
b = b - a
a = a - b

这里没有使用临时变量

# 不用临时变量的位运算版

道理和减法版相同，不过用了位运算能提高运算效率

a = a ^ b
b = b ^ a
a = a ^ b
