---
layout: post
category: python
title: "[python]Abstract Class & Abstract Method"
tags: Python abstract abstractmethod
---

# Abstract Class
* 一般用于作基类(Base Class)
* 可包含abstract method作为定义接口，由其子类实现
* Abstract Class不能创建instance
* 实现了其接口的子类可以创建instance

# 使用方法
```
from abc import ABC
from abc import abstractmethod

class MyAbstractClassWithoutAbstractMethod(ABC):
    def __init__(self):
        print('ABC without abstract method __init__ called')

class MyAbstractClass(ABC):
    def __init__(self):
        print('ABC  __init__ called')

    @abstractmethod
    def my_abstract_method(self):
        print('abstractmethod called')

class MyClassNotImplementedAbstractMethod(MyAbstractClass):
    def __init__(self):
        print('MyClass __init__ called')

class MyClass(MyAbstractClass):
    def my_abstract_method(self):
        print('Impletemented abstract method called')

if __name__ == '__main__':
    # 没有abstract method的ABC是可以创建instance的
    abc_without_abstract_method_ins = MyAbstractClassWithoutAbstractMethod()
    print('================================================')

    try:
        abc_ins = MyAbstractClass()
    except:
        print('有abstract method的ABC不能创建instance')
    print('================================================')

    try:
        ins_without_abstract_method = MyClassNotImplementedAbstractMethod()
    except:
        print('没有实现所有abstract method的类不能创建instance')
    print('================================================')

    # 实现所有abstract method的类可以创建instance并调用其中的method
    ins = MyClass()
    ins.my_abstract_method()
```

## 参考文献
* [https://docs.python.org/3.6/library/abc.html#abc.abstractmethod](https://docs.python.org/3.6/library/abc.html#abc.abstractmethod)
