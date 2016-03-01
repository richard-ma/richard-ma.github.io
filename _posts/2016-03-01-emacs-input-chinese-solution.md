---
layout: post
category: tool
title: Emacs无法输入中文问题解决方法
tags: emacs fcitx
---

当安装好Emacs后，我发现无法输入中文。Ubuntu自带的ibus输入法能够在其他软件中正常使用，但是在Emacs中就没有任何反应。

# 尝试使用ibus-el修复问题
Ubuntu14.04的软件仓库中有ibus-el这个包，据说可以解决中文输入问题，但是几经尝试，都没有成功。

# 决定使用fcitx输入法
小企鹅输入法已经有很长时间了，Ubuntu自带的ibus之前就遇到过一些问题，这次使用Emacs输入中文的问题让我下定决心更换系统提供的输入法。

## 安装小企鹅输入法

    `sudo apt-get install fcitx fcitx-sunpinyin`
    
安装好后就可以在系统设置中将默认的输入法ibus换成fcitx了。

## 设置环境变量

    `export LC_CTYPE="zh_CN.UTF-8"`

将这一行代码写入～/.profile文件中，这样无论是terminal还是一般的应用程序，就都可以读到这个环境变量了。GUI和Termial下的Emacs都可以正常工作了。
