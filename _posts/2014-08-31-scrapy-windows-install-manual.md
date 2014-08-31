---
layout: post
category: web
title: "scrapy windows install manual"
tags: python scrapy
---

# scrapy windows install manual

# 系统需求

* python 2.7
* pip
* lxml
* pywin32
* openssl

## Python

### 安装python

安装pyhton可以从python官方网站直接下载，注意版本是2.7：

[https://www.python.org/downloads/](https://www.python.org/downloads/)

### 添加环境变量

将python的`安装目录`和其下的`Scripts子目录`一起加入到*系统*的`Path`环境变量中。我的`Path`环境变量是：

C:\Python27;C:\Python27\Scripts;

### 测试环境变量是否配置成功

* 打开一个命令行窗口（运行下输入cmd）
* 输入python --version
* 若显示python版本号则环境变量设置正常；如果提示没有找到python这个命令之类的，则说明环境变量没有设置，或者路径设置错误，需要重新设置环境变量。
* 环境变量配置成功后将命令行窗口*关闭*

## pip

### 安装pip

* 到[https://bootstrap.pypa.io/get-pip.py](https://bootstrap.pypa.io/get-pip.py)下载get-pip.py脚本
* 打开一个命令行窗口并用cd命令切换到get-pip.py脚本所在的目录
* 输入python get-pip.py开始安装pip
* 提示安装完毕后即可，关闭命令行窗口

### 测试pip安装是否成功

* 打开一个命令行窗口
* 输入pip --version
* 如果看到pip版本信息，则安装成功
* 关闭命令行窗口

## lxml

### 安装lxml

* 到这里下载安装程序[http://www.lfd.uci.edu/~gohlke/pythonlibs/#lxml](http://www.lfd.uci.edu/~gohlke/pythonlibs/#lxml)
* 根据版本选择下载的文件，如我的python是`2.7`的，就下载`lxml-3.3.6.win32-py2.7.exe`这个文件
* 运行后一路下一步就可以了

## pywin32

### 安装pywin32

* 在这里下载[http://starship.python.net/crew/mhammond/downloads/](http://starship.python.net/crew/mhammond/downloads/)
* 这里也要根据python版本选择，如我的2.7版本python就对应`pywin32-217.win32-py2.7.exe`这个文件
* 运行安装程序后，一路下一步就可以了

## openssl

### 安装pyopenssl

* 首先还是下载pyopenssl程序包[https://github.com/pyca/pyopenssl/archive/0.14.zip](https://github.com/pyca/pyopenssl/archive/0.14.zip)
* 将这个zip文件解压缩
* 打开一个命令行窗口，cd到pyopenssl的目录
* 运行`pip install --user .`
* 等提示安装成功就可以关闭这个命令行窗口了

pyopenssl项目首页[https://github.com/pyca/pyopenssl](https://github.com/pyca/pyopenssl)，里面会有更多的详细信息。

# 安装scrapy

如果上面几步都顺利完成了，证明准备就绪，可以安装scrapy了。

* 打开一个命令行窗口
* 输入`pip install Scrapy`
* 提示安装成功后就可以关闭这个命令行窗口了

# 测试scrapy是否安装成功

* 打开一个命令行窗口
* 输入`scrapy`
* 看到参数介绍就说明安装成功了
