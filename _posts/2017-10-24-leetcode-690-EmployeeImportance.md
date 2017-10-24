---
layout: post
category: solution
title: "leetcode 690 Employee Importance"
tags: leetcode
---

# leetcode 690 Employee Importance

* 给出每个员工的编号,重要程度和下属列表,找出该员工的重要程度指数
* 重要程度指数是他自己和下属的重要程度指数之和

## 解法一
```
"""
# Employee info
class Employee(object):
    def __init__(self, id, importance, subordinates):
        # It's the unique id of each node.
        # unique id of this employee
        self.id = id
        # the importance value of this employee
        self.importance = importance
        # the id of direct subordinates
        self.subordinates = subordinates
"""
class Solution(object):
    def getImportance(self, employees, id):
        """
        :type employees: Employee
        :type id: int
        :rtype: int
        """
        employees = sorted(employees, key=lambda e:e.id)
        ids = [id]
        ans = 0
        for e in employees:
            if e.id in ids:
                ans += e.importance
                ids += e.subordinates
        return ans
```

## note

* 排序可以设定key参数作为多字段数据的排序关键字
