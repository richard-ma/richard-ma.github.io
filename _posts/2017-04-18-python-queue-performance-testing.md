---
layout: post
category: performance
title: "Python队列实现性能测试"
tags: python performance
---

# Python 队列性能测试

## 测试对象
Python的五种队列实现，测试其添加和删除元素的性能
* Queue Queue
* Queue LifoQueue
* Queue PriorityQueue
* Multiprocessing Queue
* Collections Deque

## 测试方法
1. 千万级别的整数作为测试数据
1. 入队、出队操作均为一千万次，全部跑完为一个测试单元
1. 每次测试时每个测试单元进行十次重复测试，计时取最大值和最小值

## 测试结果
* Queue.Queue -> min: 32.4099440575, max: 34.7603209019
* Queue.LifoQueue -> min: 33.7674992085, max: 35.7156209946
* Queue.PriorityQueue -> min: 87.2160661221, max: 92.3877229691
* Multiprocessing.Queue -> min: 78.3367807865, max: 87.1195840836
* Collections.Deque -> min: 1.67779803276, max: 1.6998360157

## 结果分析
1. 从数据量上来看，所有的队列实现都是可以满足千万元素的存储的
1. 从运行时间来看，collections.deque在性能上最优，单纯需要队列的话是首选，每秒操作次数在50w次以上。但如果需要如优先级队列等其他因素，则应该考虑其他队列实现，性能较低的队列实现每秒操作次数在10w次左右。
1. 运行时间还与计算机硬件相关，本次测试数据的机器硬件配置为i3-3240@3.4GHz/4GB，单cpu单线程
1. 在具体生产环境中，由于队列使用内存存储，且元素数量为千万级别，所以最好提前计算内存用量，以免内存耗尽。

## 测试代码
```
#!/usr/bin/env python
# encoding: utf-8

'''
测试环境：
i3-3240 @ 3.4GHz
4G memory
'''

scale = 10000000
repeatTestTimes = 10

def QueueQueue():
    from Queue import Queue
    q = Queue()
    for i in range(scale):
        q.put(i)
    for i in range(scale):
        q.get()

def QueueLifoQueue():
    from Queue import LifoQueue
    q = LifoQueue()
    for i in range(scale):
        q.put(i)
    for i in range(scale):
        q.get()

def QueuePriorityQueue():
    from Queue import PriorityQueue
    q = PriorityQueue()
    for i in range(scale):
        q.put(i)
    for i in range(scale):
        q.get()

def MultiprocessingQueue():
    from multiprocessing import Queue
    q = Queue()
    for i in range(scale):
        q.put(i)
    for i in range(scale):
        q.get()

def CollectionsDeque():
    from collections import deque
    q = deque()
    for i in range(scale):
        q.append(i)
    for i in range(scale):
        q.pop()

if __name__ == '__main__':
    from timeit import Timer

    tt = Timer("QueueQueue()", "from __main__ import QueueQueue")
    repeatTimeList = tt.repeat(repeatTestTimes, 1)
    print "Queue.Queue -> min: %s, max: %s" % (min(repeatTimeList), max(repeatTimeList))

    tt = Timer("QueueLifoQueue()", "from __main__ import QueueLifoQueue")
    repeatTimeList = tt.repeat(repeatTestTimes, 1)
    print "Queue.LifoQueue -> min: %s, max: %s" % (min(repeatTimeList), max(repeatTimeList))

    tt = Timer("QueuePriorityQueue()", "from __main__ import QueuePriorityQueue")
    repeatTimeList = tt.repeat(repeatTestTimes, 1)
    print "Queue.PriorityQueue -> min: %s, max: %s" % (min(repeatTimeList), max(repeatTimeList))

    tt = Timer("MultiprocessingQueue()", "from __main__ import MultiprocessingQueue")
    repeatTimeList = tt.repeat(repeatTestTimes, 1)
    print "Multiprocessing.Queue -> min: %s, max: %s" % (min(repeatTimeList), max(repeatTimeList))

    tt = Timer("CollectionsDeque()", "from __main__ import CollectionsDeque")
    repeatTimeList = tt.repeat(repeatTestTimes, 1)
    print "Collections.Deque -> min: %s, max: %s" % (min(repeatTimeList), max(repeatTimeList))
```
