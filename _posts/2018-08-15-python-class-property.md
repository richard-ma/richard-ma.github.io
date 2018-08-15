---
layout: post
category: python
title: "[python]类的property"
tags: Python property
---

# Property
* `@property`可以用于修饰一个python类的成员方法
* 主要用途就是弥补ptyhon类成员变量没有访问控制（public protected private)
* python默认的成员变量全部是public

# 使用方法
```
class WithoutProperty:
    def __init__(self):
        self._temperature = 20

class WithProperty:
    def __init__(self):
        self._temperature = 20

    @property
    def temperature(self):
        return self._temperature

class CompletedProperty:
    def __init__(self):
        self._temperature = 20

    @property
    def temperature(self):
        print('call temperature.getter')
        return self._temperature

    @temperature.setter
    def temperature(self, value):
        print('call temperature.setter')
        self._temperature = value

    @temperature.deleter
    def temperature(self):
        print('call temperature.deleter')

if __name__ == '__main__':
    # 没有使用property
    without_property = WithoutProperty()
    print(without_property._temperature) # 输出默认值20
    without_property._temperature = 35 # 可以给成员变量赋值
    print(without_property._temperature) # 输出新值35

    # 使用Property
    with_property = WithProperty()
    print(with_property._temperature) # 仍然可以使用，但已经不作为接口
    print(with_property.temperature) # 输出默认值20，这里temperature是一个属性
    try:
        with_property.temperature = 35 # 无法赋值
    except:
        print('无法赋值')

    # 完整的Property
    completed_property = CompletedProperty()
    print(completed_property.temperature) # 调用getter
    completed_property.temperature = 35 # 调用setter 可以赋值
    print(completed_property.temperature) # 调用getter 查看新值
    del completed_property.temperature # 调用deleter
```

# TIPS
* WithoutProperty类没有使用property，其成员变量\_temperature是public的
* WithProperty类仅仅设置了getter，所以temperature只能读取不能修改赋值
* CompletedProperty类给出了getter、setter和deleter，这是property的完整形式，可读取可修改赋值，还可以删除

# 参考文献
* [https://blog.csdn.net/AlanGuoo/article/details/78855750](https://blog.csdn.net/AlanGuoo/article/details/78855750)
* [https://docs.python.org/3.6/library/functions.html?highlight=property#property](https://docs.python.org/3.6/library/functions.html?highlight=property#property)
