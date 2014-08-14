---
layout: post
category: rails
title: "[Date with Rails] 将erb转换为slim"
tags: ruby rails
---

# 为什么有这个需求

写过PHP的朋友大多知道，最早的动态页面模板其实就是HTML代码和模板语言的大杂烩，例如PHP社区著名的Smarty模板框架。rails的模板最初也是这种原始状态，即erb模板。erb模板本质就是ruby代码和HTML代码合体的结果。随着人们对于HTML标签配对的厌恶和大量重复的无趣代码，社区逐渐发展除了haml和以及其升级版slim。这两种都对HTML代码部分做了简化，也应用了一些JQuery中的CSS选择器思想，让HTML代码尽量减少重复。

我开始学习rails时写了一个用erb模板的项目，后来在社区听说了slim。一看语法果然简洁好多，不过木已成舟，我的那些erb模板代码如何升级成slim模板呢？下面就是我解决这个问题的一个记录。

# 转换思路

由于slim是由haml演变来的，而haml是对erb的一次简化，那么我们就遵循这条路径来进行升级替换。

    erb -> haml -> slim

# 工具

这里需要两个gem包，html2haml和haml2slim。从名字就可以看出这两个包的作用：

* html2haml - 将html（erb）模板转换为haml格式模板
* haml2slim - 将haml模板转换为slim格式模板

安装这两个工具直接使用gem即可：

`gem install html2haml haml2slim`

    注意他们工作依赖libxml2和libxslt，确保你系统里已经安装了这两个包。

# 实做

## 小心使得万年船

如果你的项目已经使用了版本控制系统，那么我建议你在实做前进行一次提交。如果没有使用版本控制系统，我建议你先学习一下，防止转换结果不能工作，而让你之前的努力付之东流。

不过总有个偷懒的办法，就是备份`/app/views/`目录及子目录下的所有erb模板文件。用这个命令可以找到所有erb模板文件，形成一个清单：

`find . -name '*html.erb'`

## 转换

### 将erb转换为haml

`find . -name '*html.erb' | xargs ruby -e 'ARGV.each { |i| puts "html2haml -r #{i} #{i.sub(/erb$/,"haml")}"}' | bash`

### 将haml转换为slim

`find . -name '*html.haml' | xargs ruby -e 'ARGV.each { |i| puts "haml2slim #{i} #{i.sub(/haml$/,"slim")}"}' | bash`

## 清理

### 删除erb文件

`find . -name '*html.erb' | xargs rm`

### 删除haml文件

`find . -name '*html.haml' | xargs rm`

## 测试

打开你的`rails server`，看看网页是否能正常工作吧！当然，可以跑一遍对于controller的单元测试是更加严谨的做法。

# 原文链接（英文）

[http://www.22ideastreet.com/blog/2011/10/19/converting-erb-to-slim/]
