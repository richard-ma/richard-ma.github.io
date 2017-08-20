---
layout: post
category: solution
title: "leetcode 506 Relative Ranks"
tags: leetcode
---

# leetcode 506 Relative Ranks

## 解法一

```
class Solution(object):
    def findRelativeRanks(self, nums):
    """
    :type nums: List[int]
    :rtype: List[str]
    """
    sorted_nums = sorted(nums, reverse=True)
                                                   
    for k, v in enumerate(sorted_nums):
        nums[nums.index(v)] = str(k+1)
                                                                             
    if len(nums)>0:
        nums[nums.index("1")] = "Gold Medal"
    if len(nums)>1:
        nums[nums.index("2")] = "Silver Medal"
    if len(nums)>2:
        nums[nums.index("3")] = "Bronze Medal"

    return nums
```

## note
* 使用list.index(value)可以找出value对应的index
* sorted中的reverse设置为True可以降序排列

## 解法二

```
def findRelativeRanks(self, nums):
    sort = sorted(nums)[::-1]
    rank = ["Gold Medal", "Silver Medal", "Bronze Medal"] + map(str, range(4, len(nums) + 1))
    return map(dict(zip(sort, rank)).get, nums)
```

## note
* rank为金银铜牌和4到末尾的名次列表
* zip函数将两个数量相等的list合并为一个二元组的list zip([x, y, z], [1, 2, 3]) => [(x, 1), (y, 2), (z, 3)]
* dict.get函数根据给出的参数作为key,返回对应的key的value
* 这里将排序好的数据作为key,将名次作为value,用Map查询每个nums里的数据对应的名次,以list返回
