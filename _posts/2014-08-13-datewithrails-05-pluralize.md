---
layout: post
category: rails
title: "[Date with Rails] 名词复数是怎么转换的"
tags: ruby rails
---

# 神奇的复数

上一篇我提到了调戏rails复数的一个小测试，有很多读者反映这个功能很神奇，那么rails是如何实现这个功能的呢？这确实是个值得研究的好问题！

# 字符串的特殊功能

在rails框架中的字符串，都有一个方法叫做：pluralize，这就是将字符串翻译为复数的方法，返回英语名词的复数形式。为什么是强调在rails框架中呢？因为ruby默认的字符串并没有这个方法，为了证明这一点我们可以做一个小实验。

## irb

先打开ruby默认的交互shell `irb`，输入如下命令：

`'post'.pluralize`

会提示字符串并没有pluralize方法。证明pluralize方法对于ruby原生的String类并不存在。

## rails c

接着可以打开rails提供的console `rails c`，输入同样的命令：

`'post'.pluralize`

会看到返回了`'posts'`，证明在rails框架中的String类有pluralize方法。

很明显，`pluralize`方法是rails在框架中对原生的String类扩展出来的方法。

# pluralize如何被扩展出来

看懂这部分需要对ruby元编程有一点小知识，当然如果您是lisp高手这部分就是小菜一碟了。这个扩展pluralize的方法叫做`打开类`。

ruby是动态语言，对于类的操作这部分我觉得可能是参考了lisp。闲话少说，先来看看ruby对于`打开类`是如何做到的。

## 打开类

简单来说一般的面向对象语言是不允许重复定义类的，但在ruby和lisp中是可以的，重复定义类实际是对类的内部做了追加和替换。

例如有一个名叫Person的类，在第一次定义的时候有一个`eat`方法，这是类的方法可以简单表示为：

    Person
      eat()

在Person类定义后，第二次定义Person类，并且定义一个`sing`方法，那么现在的Person类可以简单表示为：

    Person
      eat()
      sing()

我们看到第二次定义实际是给Person类添加了一个新方法，这种扩展类功能的方法就是`打开类`了。

## 为String扩展pluralize方法

刚刚说到所有英语名词字符串复数形式都是通过pluralize方法获得的，那么必须对ruby原生的String类扩展出一个pluralize方法。实现的技术就是上面提到的ruby中`打开类`的扩展形式。也就是在rails框架中重新定义String类，并且定义pluralize方法。

除了pluralize方法，rails还对ruby原生的String类扩展了一些方法，具体代码可以看这里：

https://github.com/rails/rails/blob/master/activesupport/lib/active_support/core_ext/string/inflections.rb#L31

下面是函数中的关键语句：

    ActiveSupport::Inflector.pluralize(self, locale)

从这段代码可以看出，转换复数的工作交给了`ActiveSupport::Inflector`中的`pluralize`方法。至此我们知道了pluralize方法是rails框架通过`打开类`的方式为String类扩展出来的方法。

# ActiveSupport::Inflector

`ActiveSupport`是一个module，`Inflector`也是一个module。下面便是`pluralize`方法的代码：

https://github.com/rails/rails/blob/master/activesupport/lib/active_support/inflector/methods.rb#L31

这个方法比较简单，将所有工作交给了`apply_inflections`方法。传入了有待转换复数的字符串`word`和语言对应的转换复数函数`inflections(locale).plurals`。

## apply_inflections

这个方法先检查传入的word是否为empty或者是否为不可数名词，如果满足这两点之一，那么直接返回这个word。

如果可数名词则逐个检查传入的第二个参数的规则列表，实质是匹配名词的正则，有匹配的就进行相应的替换操作，将名字变为复数形式。这部分代码在这里：

https://github.com/rails/rails/blob/master/activesupport/lib/active_support/inflector/methods.rb#L378

# 神奇的替换规则

这部分其实是实现名词变复数的关键所在，有一部分正则表示的规则和一个特例表组成：

正则替换规则： https://github.com/rails/rails/blob/master/activesupport/lib/active_support/inflections.rb#L11

特例表：https://github.com/rails/rails/blob/master/activesupport/lib/active_support/inflections.rb#L61

## 规则列表

规则列表可以理解为一个两列的列表，第一列是名词特征的正则表达式，第二列是将其变为复数的替换规则正则表达式。

| 名词特征             | 替换规则                   | 规则说明                        |
|----------------------|----------------------------|---------------------------------|
| /$/                  | 's'                        | 将所有单词的结尾后加s           |
| /sis$/i              | 'ses'                      | 以sis结尾的单词替换为ses        |

## 添加规则

这里的正则存放在一个block中，每次block获得一个`Inflector.inflections(:en)`用yield返回的`inflect`对象。利用这个block不断的将名词匹配规则和复数形式替换规则添加到规则列表中。这部分代码参见：

https://github.com/rails/rails/blob/master/activesupport/lib/active_support/inflector/inflections.rb#L203

而`inflect`对象是由`Inflections.instance(locale)`创建的，这部分代码参见：

https://github.com/rails/rails/blob/master/activesupport/lib/active_support/inflector/inflections.rb#L30

创建过程中有这样一句：
    
    @__instance__[locale] ||= new

这里使用了设计模式中的`singleton pattern`（中文一般为“单例模式”）。实质是将变复数规则添加到了一个名为`@plurals`的list当中，在名词变复数的时候就在这个list中逐个匹配名词特征，如果匹配成功就进行相应的替换操作，将名词变为复数形式。

# 后记

rails框架将名词变为复数的机制并不是什么高新技术，但要做到规则的有序管理和精确替换确实不容易，从规则列表来看也是很多人的智慧结晶。这次hack看到了一些设计模式和ruby meta programming的具体应用，感觉还是有些许收获的。在规则列表的注释可以看出，替换规则现在一个`freeze`了。上面提到虽然这个规则列表不能做到完全正确，但为了保证现有rails程序的正常运行，所以开发者们不会在修改了，工业上也是有许多缺憾美的。

# 感谢

* 感谢冯添提出了这么好的一个问题
* 感谢姜军给我指明了rails实现复数功能位于activesupport这个部分，并且指出是正则和特例表的实现方法
