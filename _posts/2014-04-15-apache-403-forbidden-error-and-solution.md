---
layout: post
category: web
title: Apache 403 禁止访问排查方法
tags: http Apache 403
---

当Apache出现403禁止访问错误的时候，往往是权限问题导致的，所以可以按照如下方法排查问题。

#  用户名和密码是否正确

如果网站确实需要认证才可以访问页面，核对一下用户名和密码的正确性确实很有必要。

#  没有Apache DirectoryIndex项目中的文件

当没有默认首页文件时，同时又不可以浏览目录内容，这样的配置会导致403错误。

如果不知道默认首页文件名，可以查阅Apache配置文件中的DirectoryIndex项目设置。

> DirectoryIndex index.html index.cgi index.pl index.php index.xhtml

#  检查CGI文件是否有可执行权限

如果用到CGI文件，其应有对应的可执行权限。如果没有可执行权限，可以使用以下命令添加。

> $ chmod +x file.cgi

#  是否有.htaccess使用权限

如果目录中有.htaccess文件，而Apache配置文件禁用了.htaccess使用权限，就会发生403错误。

#  保证目录有正确的权限

请确认Apache配置文件中的目录权限如下所示，当然你的目录可能有特殊配置，不过要明确是否对于用户和访问。

> <Directory "/home/domain/www">
> 
>     Options +Indexes FollowSymLinks +ExecCGI
> 
>     AllowOverride AuthConfig FileInfo
> 
>     Order allow,deny
> 
>     Allow from all # 我的问题就是这里，原来写成Deny for all了，就出现了403错误
> 
> </Directory>

#  确保目录都有文件系统可执行权限

Linux文件系统权限中，目录必须具有可执行权限内容才能被访问到。如果Apache目录没有可执行权限，那么里面的文件也无法访问，就会发生403错误。

可以使用以下命令给目录添加可执行权限

> chmod +x /home/httpd/theos.in/

#  察看Apache错误日志寻找原因

最后的方法就是察看Apache错误日志来寻找403的原因，日志文件路径如下：

> /var/log/apache2/error.log #这里是默认错误日志的路径，不过不同的发行版可能路径稍有区别

<a href="http://www.cyberciti.biz/faq/apache-403-forbidden-error-and-solution/" target="_blank">英文原文</a>
