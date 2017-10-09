---
layout: post
category: solution
title: "leetcode 83 Remove Duplicates From Sorted List"
tags: leetcode
---

# leetcode 83 Remove Duplicates From Sorted List

* 删除已排序链表中的重复元素

## 解法一
```
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        curr = head
        while curr != None and curr.next != None:
            if curr.val == curr.next.val: # 发现重复值，跳过，但curr不移动，继续检测后面的值还有没有重复的
                curr.next = curr.next.next
            else:
                curr = curr.next # 值不同，curr后移
        return head
```

## note

* 删除元素就是将前一个指针直接指向下一个元素即可，从链表将该元素摘下来
* 如果有重复元素，curr指针不应该后移，要继续检测后面是否还有重复的元素
