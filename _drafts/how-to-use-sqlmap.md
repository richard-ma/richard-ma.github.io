---
layout: post
category: hacker
title: 如何使用sqlmap
tags: sql injection sqlmap
---

# 简介

sqlmap是一个自动化的sql注入（sql injection）工具。可以自动探测漏洞，并利用漏洞实施sql注入攻击，甚至可以从Google搜索结果中寻找攻击目标。更加不可思议的是，它自带一个网络爬虫（crawler），方便寻找sql注入点。

# 下载与安装

## 下载地址

<a target='_blank' href='http://sqlmap.org'>http://sqlmap.org</a>

## 系统需求

sqlmap是一个python编写的工具，可以在装有python 2.6.x或2.7.x的任意系统平台上运行。

## 安装方法

这里以Linux系统为例，解压后即可使用，无须安装：

    $ tar -xvzf sqlmap-xxxxxxx.tar.gz
    $ cd sqlmap-xxxxxxx

目录中有一个sqlmap.py文件，这就是我们要用的工具了。

# 使用讲解

现在当然想迅速找到sql注入漏洞了，不过真正关注安全的互联网网站，sql注入漏洞是不容易寻找的。即使是个人搭建的网站，如果使用了成熟的开源系统，也是不容易发现漏洞的。

综上我建议大家自己写一个有漏洞的页面，这样学习起来会比较方便。如果没有，我给大家准备了一个写好的小网站，只有两个页面，列出了数据库中虚构的一些用户名和密码。

可以到这里下载：<a target='_blank' href='https://gitcafe.com/richard-ma/sql-injection'>sql-injection</a>

*attack-site*目录下就是有漏洞的网站代码了，需要你有一个能运行php和mysql的环境。

## 小试牛刀


