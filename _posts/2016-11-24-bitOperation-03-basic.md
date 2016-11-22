---
layout: post
category: bitOperation
title: "[说说位运算] 基本位运算操作"
tags: bit algorithm
---

# 从低位到高位，取n的第m位

(n >> (m-1)) & 1

# 从低位到高位，将n的第m位置1

n | (1 << (m-1))

# 从低位到高位，将n的第m位置0

n & ~(1 << (m-1))

# Tips

某位设置为0的方法是先将其设置为1，然后取反将其置为0
