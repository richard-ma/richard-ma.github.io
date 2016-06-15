---
layout: post
category: tool
title: vim UltiSnips requires py >= 2.6 or any py3
tags: vim python
---

在Ubuntu 16.04安装好vim包后提示`UltiSnips requires py >= 2.6 or any py3`。在vim中运行`:py`命令提示没有这个命令，显然这个报错虽然是UltiSnips插件报的，但是根本原因是这个vim包在编译的时候没有添加对python的支持。

# 尝试搜索错误信息
遇到问题的第一反应就是把错误信息写到搜索引擎里，得到Stack Overflow的回答是要在configure时加入参数`./configure --enable-pythoninterp`。

很显然这是要加入python支持的编译选项，不过deb包是编译好的，如果这个vim包没有，那么一定有个有python支持的包。

# 搜索带python支持的vim包

使用`apt-cache search vim`命令搜索所有vim相关的包，通过查看简要介绍发现这样一行`vim-nox-py2 - Vi IMproved - enhanced vi editor - with scripting languages support (Python2)`。

这个`vim-nox-py2`是支持python的，同时还有一个`vim-nox`包，声称支持脚本语言，估计是安装后其他语言写的插件才可以使用，暂时没有安装。
