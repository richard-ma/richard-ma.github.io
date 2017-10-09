---
layout: post
category: solution
title: "leetcode 206 Reverse Linked List"
tags: leetcode
---

# leetcode 206 Reverse Linked List

* 将链表反序

## 解法一 递归
```
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head == None or head.next == None: # 有0个或1个元素的链表
            return head
        else:
            p = self.reverseList(head.next) # 获得新表头
            head.next.next = head # head.next是表尾 将head放在它后面，成为新表尾
            head.next = None # 将表尾next设置为None
            return p # 返回新表头
```

## 解法二 迭代
```
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        prev = None # 初值是队尾
        curr = head 
        while curr != None:
            t = curr.next # 记录未处理指针
            curr.next = prev # 反向指向前一个元素
            prev = curr # 后移prev
            curr = t # 后移curr
        return prev # 返回新head
```

## note
* 有递归和迭代两种解法
