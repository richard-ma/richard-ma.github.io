---
layout: post
category: solution
title: "leetcode 141 Linked List Cycle"
tags: leetcode
---

# leetcode 141 Linked List Cycle

* 检查链表中是否有环

## 解法一

* 每次访问一个节点做记录，并查找当前节点是否在访问过的节点列表中出现
* 空间需要O(n)

## 解法二
```
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        if head == None or head.next == None:
            return False # 有0个或1个元素的链表不可能出现环
        
        slow = head
        fast = head.next
        while fast != slow:
            if fast == None or fast.next == None: # fast指针到达链表尾，则没有环
                return False
            slow = slow.next
            fast = fast.next.next
            
        return True # fast指针追上slow指针，证明有环
```

## note

* 快慢指针追逐法
    * slow指针每次移动一个元素，fast指针每次移动两个元素
    * 若fast指针到了队尾，则不存在环
    * 若fast指针追上了slow指针，则存在环
