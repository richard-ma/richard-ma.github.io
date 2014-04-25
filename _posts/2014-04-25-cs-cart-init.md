---
layout: post
category: source-reading 
title: cs-cart 启动过程
tags: cs-cart
---

序：本文使用的cs-cart版本为4.1.2

# 入口文件

cs-cart是一个多入口的系统，目前为止有index, admin和api三个入口，对应如下请求：

* index.php 商店前台，普通用户浏览购买商品
* admin.php 管理员后台，对于网站管理员的管理入口
* api.php API调用入口，用于相应对API的调用

入口文件定义了AREA常量，A表示admin，C表示Customer，而API则定义了API常量和NO_SESSION常量来表示是API调用。

注：API未来可能有改动，这里简单介绍。

# 处理流程

当一个request到来的时候，会经历如下处理流程：

入口文件 --> init.php --> controller/action

cs-cart的主要初始化部分在init.php中完成，例如各读取配置文件、模块的初始化、链接数据库、调试器的初始化等等。

在init.php中的fn_dispatch()函数中分发到controller中继续处理。

# 配置文件

配置文件有两个：

* config.php 系统配置，主要是一些系统的常量定义，一般不需要用户修改
* config.local.php 网站域名，数据库主机用户以及密码等用户配置信息，需要修改为适当的值

init.php加载配置时只加载config.php，而config.local.php是被config.php使用require函数加载进去的。如下图：

init.php <-- config.php <-- config.local.php

# 核心模块

核心模块被单独写成了函数库，存放在app/functions中。

这些核心模块将在后面单独分析。
