---
layout: post
category: system administration
title: kworker进程吃掉了我全部CPU
tags: acpi driver compiz
---

# 起因

前几天突然觉得我的Ubuntu运行的比以往慢了很多，top后发现一个叫kworker的进程占用了将近80%的CPU。这显然是不正常的，而且这种速度基本就没法用了，所以就有了后面的故事。

# 重装

一开始是怀疑最近更新的包中有BUG导致的，结果重装了Ubuntu 14.04。好在我自己有个重装系统的脚本，算上更新系统和回复环境，一小时搞定。

# 继续追踪

重装后的系统应该是干净的，结果发现无论更新前还是更新后，kworker的CPU占用率一直居高不下，看来不是新包引入的BUG。

向TJLUG的邮件列表求助后，mikeandmore告诉我可以使用perf工具分析下，看看是那个函数占用了过多的CPU时间。

经过数据的收集和分析，看来是acpi的问题。

# 解决

在grub启动选项中加入了acpi=off这个参数，关闭acpi。

重启后发现kworker的CPU占用率下来了！不过compiz的CPU占用率又上到了80%以上，这次我怀疑是显卡驱动问题。

直接安装了nvidia的最新驱动：nvidia-current

重启后一切正常了。

本着要弄清问题本质的想法，我又开启了acpi，重启后发现kworker的CPU占用率又上升到80%左右。

至此问题的症结找到了，就是acpi。

# 经验和总结

1. perf在分析上帮了大忙，将问题锁定在acpi上
1. compiz的问题大多和显卡驱动有关，所以新装系统即使能用也不能忽视显卡驱动的问题
1. 私有驱动就是比开源驱动效率高，谁让硬件是人家做的呢，软件自然做得好
