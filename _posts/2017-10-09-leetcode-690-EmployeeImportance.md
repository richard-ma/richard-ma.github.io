---
layout: post
category: solution
title: "leetcode 690 Employee Importance"
tags: leetcode
---

# leetcode 690 Employee Importance

* 员工重要程度为他自己和所有下属的重要程度之和

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
        
        ans = 0
        subs = [id]
        for e in employees:
            if e.id in subs:
                ans += e.importance
                subs += e.subordinates
                
        return ans
```

## note

* 员工id都是排好序的
* 雇佣关系是树
* bfs
