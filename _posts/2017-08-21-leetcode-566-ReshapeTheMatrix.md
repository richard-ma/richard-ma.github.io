---
layout: post
category: solution
title: "leetcode 566 Reshape The Matrix"
tags: leetcode
---

# leetcode 566 Reshape The Matrix

* 将二维list的列数m转换为n的新矩阵
* 如果不能转换，则原list不变输出

## 解法一
```
class Solution(object):
    def matrixReshape(self, nums, r, c):
    """
    :type nums: List[List[int]]
    :type r: int
    :type c: int
    :rtype: List[List[int]]
    """
    flat = sum(nums, [])
    if len(flat) != r * c:
        return nums
    tuples = zip(*([iter(flat)] * c))
    return map(list, tuples)
```

## note
* sum就是简单的将元素相加，但nums的元素是list，list对于加号是连接的意思：[1, 2] + [3] = [1, 2, 3]
* 这里sum使用第二个参数[]，是为了表明元素是list，否则sum无法处理[[], []]这种格式的数据
* 第二和第三行比较容易理解，是判断nums是否可以被重新组织成r行c列的模式
* iter函数返回一个flat的迭代器，相当于一个指针吧
* [iter(flat)] * c是对迭代器的使用，如果flat是[1, 2, 3]而c是3的话，迭代器的指针分别指向1, 2, 3
* zip(*([iter(flat)] * c)) *是任意多个参数传递给zip，参数为c个flat数组的迭代器，每次zip调用一次迭代器则会自动next一次，这样就实现了取c个元素的操作
* map(list, truples) 是对truples的每个元素使用list函数变为一个lilst，符合题意

## 解法二：
```
def matrixReshape(self, nums, r, c):
    if r * c != len(nums) * len(nums[0]):
        return nums
    it = itertools.chain(*nums) # 将nums变为一维数组
    return [list(itertools.islice(it, c)) for _ in xrange(r)] # 以c为单位进行划分
```

## note
* 廖雪峰的blog： https://www.liaoxuefeng.com/
