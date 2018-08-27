---
layout: post
category: python
title: "[python]从类名创建对象"
tags: Python instance
---
# eval

* 类名加上括号直接用eval执行

```
class A():
  pass

a = eval('A()') # A()直接被执行，生成一个A类的instance
```

# getattr

* 使用__import__和getattr加载类

```
module = __import__(file_name) # file_name为文件名
parser = getattr(module, class_name)() # 创建instance
parser.method_name() # 调用instance的方法
```

# 参考文献
* [https://blog.csdn.net/geekster/article/details/17093623](https://blog.csdn.net/geekster/article/details/17093623)
