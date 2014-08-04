---
layout: post
category: rails
sid: 2
title: "[Date with Rails] 配置的约定"
tags: ruby rails
---

# 配置的约定

## 配置文件在哪里？

书接上回~~我们提到了/config目录中保存着应用和数据库连接的一些配置文件，这就是本篇的主角了，我们来一探究竟吧。

* /config
* application.rb 应用启动前运行的代码（不用修改）
* environment.rb 应用启动前运行的代码（不用修改）
* boot.rb 应用启动前运行的代码（不用修改）
* database.yml 数据库连接的参数
* routes.rb URL与controller的映射关系（有特殊需要时修改）
* environments/ 不同环境下的配置开关，稍后会介绍Rails的运行环境
* initializers/ 应用初始化的一些配置
* locales/ 关于L10N本地化的翻译文件

## Rails的运行环境

Rails为不同的目的提供了不同的配置参数，在/config/environments/目录下有三个不同的文件，代表了三种不同的Rails运行模式：

* development.rb 开发环境
* test.rb        测试环境
* production.rb  生产环境

在应用开发的过程中，我们往往会用到不同的配置。开发过程中我们希望所有的Debug功能都开启，log记录尽量详细，总是加载最新的文件而不要使用缓存等等。测试中我们希望所有的问题都是可重复的，方便我们查找bug。而正是上线后的生产环境则是相反的要关闭这些不必要的功能，性能为先。

默认的三个文件配置能够满足绝大部分需求，当你有特殊需求的时候记得修改对应的文件。

* rails server 使用development.rb的环境
* rake test 使用test.rb的测试环境
* rails server -e production 使用production.rb性能为先的生产环境

可以在rails server命令后加上-e参数来设置运行环境的名称：

`$ rails server -e environment_name`

注：environment_name可以替换成test, production, development

## 连接数据库

Rails对于数据库的操作已经完全抽象到几乎不需要使用SQL的程度了，当然Rails对于数据库的支持也是非常全面的，我常用的有postgresql, sqlite, mysql三种，不过支持的绝对不是这三种而已。详细列表请猛戳这里： [Google](http://www.google.com)。是的您没有看错，目前我没有找到详细的Rails数据库支持列表。原因不是因为Rails支持的种类少，相反应该是支持的种类很多，具体配置方法请您根据需要Google一下。

Rails默认的数据库是sqlite，这是个不错的主意，因为它够小也够快。开发和测试的时候往往不需要做压力测试，所以选择一个轻量的数据库是个好想法。

打开/config/database.yml文件会看到三个不同的配置段落，当然这对应上一节提到的三种运行环境。这里需要注意的地方有两点：

* 你可以对不同的运行环境使用不同的数据库，这都是自由并且互相没有干扰的
* 对于test环境下使用的数据库，对应的数据库账户必须有创建和删除数据库的权限。由于test环境要保证测试可重复性，所以会经常用删除数据库的形式初始化一个相对干净的测试环境

## 总结

现在已经把数据库配置好了，下一步我们就可以创建一个简单的应用，这才是真正见证Rails开发速度的时刻！
