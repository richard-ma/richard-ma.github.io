---
layout: post
category: solution
title: "leetcode 203 Remove Linked List Elements"
tags: leetcode
---

# leetcode 203 Remove Linked List Elements

* 删除链表中的指定值

## 解法一
```
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def removeElements(self, head, val):
        """
        :type head: ListNode
        :type val: int
        :rtype: ListNode
        """
        prev = head_node = ListNode(val+1)
        prev.next = head
        curr = head
        while curr != None:
            if curr.val == val:
                prev.next = curr.next
            else:
                prev = prev.next
            curr = curr.next
        
        return head_node.next
```

## note

* 添加头节点简化算法
* 返回头节点的next作为结果链表的head
