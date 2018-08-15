---
layout: post
category: python
title: "[python]类中的几种方法"
tags: Python classmethod staticmethod
---

# [python]类中的几种方法

## instance method
实例是用类作为模板创建出来的具体对象，python中每个instance method都需要传入一个默认参数self，利用self可以引用类中定义的各种变量和方法

## class method
类方法会传入一个cls参数，这个参数代表类本身

## static method
静态方法和普通函数一样，只不过属于一个特定的类，类之外无法调用

## 定义和调用
```
class MyClass():

    def method(self):
        return "instance method called", self

    @classmethod
    def classmethod(cls):
        return "class method called", cls

    @staticmethod
    def staticmethod():
        return "static method called"

if __name__ == '__main__':
    ins = MyClass()

    print(ins.method())
    print(ins.classmethod())
    print(ins.staticmethod())

    print(MyClass.classmethod())
    print(MyClass.staticmethod())
    print(MyClass.method()) # Error 类不能调用instance method，因为没有实例
```

## class method实现工厂类
```
class Pizza():
    def __init__(self, ingredients):
        self.ingredients = ingredients

    def __repr__(self): # 输出list类型的变量
        return f'Pizza({self.ingredients!r})'

    # classmethod可以方便的创建factory设计模式
    @classmethod
    def margherita(cls): # 一种Pizza配方
        return cls(['mozzarella', 'tomatoes']) # 直接返回Pizza实例

    @classmethod
    def prosciutto(cls): # 另一种Pizza配方
        return cls(['mozzarella', 'tomatoes', 'ham'])

if __name__ == '__main__':
    ins1 = Pizza.margherita()
    ins2 = Pizza.prosciutto()

    print(ins1) # 调用__repr__输出配方内容
    print(ins2) # 调用__repr__输出配方内容
    print(isinstance(ins1, Pizza)) # ins1是由Pizza生成
    print(ins1.__class__) # ins1的类名，应该是Pizza
```

## static method定义类中的helper
```
class Pizza():
    def __init__(self, radius, ingredients):
        self.radius = radius
        self.ingredients = ingredients

    def __repr__(self): # 输出list类型的变量
        return f'Pizza({self.ingredients!r})'

    def area(self):
        return self.circle_area(self.radius) # 内部调用helper方法，要用self

    @staticmethod
    def circle_area(r): # 计算圆形面积，不需要每个实例都有，是helper方法
        return r ** 2 * math.pi

if __name__ == '__main__':
    p = Pizza(4, ['mozzarella', 'tomatoes'])
    print(p.area()) # 计算instance的面积
    print(Pizza.circle_area(4)) # 类外部调用
```
