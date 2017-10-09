---
layout: post
category: solution
title: "leetcode 21 Merge Two Sorted Lists"
tags: leetcode
---

# leetcode 21 Merge Two Sorted Lists

* 将两个排序的链表按顺序合并

## 解法一
```
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        head = p = None
        p1 = l1
        p2 = l2
        
        if not (p1 and p2):
            return p1 or p2
        
        while p1 != None and p2 != None:
            curr = None
            if p1.val <= p2.val:
                curr = p1
                p1 = p1.next
            else:
                curr = p2
                p2 = p2.next
                
            if head == None:
                head = p = curr
            else:
                p.next = curr
                p = curr
                p.next = None
                
        if p1 != None:
            p.next = p1
        elif p2 != None:
            p.next = p2
            
        return head
```

## note
* 合并后有一个链表可能还有尾部需要链接到新链表
* 有一个链表为空的初始情况，需特殊处理
* a or b在Python中表示 a == None 时则使用b的值
