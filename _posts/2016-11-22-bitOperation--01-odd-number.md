---
layout: post
category: bitOperation
title: "[说说位运算] 判断奇偶数"
tags: bit algorithm
---

# 朴素算法

1. N % 2 == 0 对2取余，如果结果为0则N是偶数，否则为奇数

# 位运算版本

1. (N & 1) == 0 按位与1，结果为0则是偶数，否则为奇数
