---
layout: post
category: source-reading 
title: cs-cart Bootstrap::initEnv 
tags: cs-cart
---

# fixServerVars 调整$server的某些元素

* 检查$server['HTTP_HOST']是否设置，如没有使用localhost
* 如设置了$server['HTTP_X_REWRITE_URL']则说明使用了is_apirewrite，则将其赋值给$server['REQUEST_URI']
* 使用stripslashes和删除单引号和双引号过滤$server['QUERY_STRING']，防止SQL注入攻击
* PHP_AUTH_USER PHP_AUTH_PW相关设置

# setConstants 设置运行时常量

常量                    |意义                       |默认值
------------------------|---------------------------|---------------------------
TIME                    |时间（单位为秒）           |当前时间 time()
MICROTIME               |时间（单位为微秒）         |当前时间 microtime(true)
MIN_PHP_VERSION         |最低的PHP版本              |5.3.0
CHARSET                 |字符集                     |utf-8
BOOTSTRAP               |是否使用Bootstrap          |true
QUOTES_ENABLE           |是否开启magic_quote        |PHP配置
IS_WINDOWS              |是否运行在Windows下        |自动探测
REAL_HOST               |主机IP                     |自动探测
REAL_URL                |真实的链接地址             |自动组装
DIR_ROOT                |根目录                     |自动探测（自动替换win下的反斜杠）

* 当没有zlib时，如果开启了压缩，则使用gzip压缩
* 检测PHP版本是否达到最低要求，如果没有则给出相应升级提示

# detectHTTPS

* 通过$server判断是否开启HTTPS模式

# setConfigOptions 修改PHP设置项目

* magic_quotes_sybase = 0
* 添加pear到include_path中
* pcre.backtrack_limit 限制Perl正则的回溯
* arg_separator.output 将PHP生成的URL参数分隔符设置为&
* ignore_user_abort设置为true，在浏览器断开后，仍可以执行脚本剩余部分，这样便可以保证脚本不会突然被终止，可以进行适当的清理

Session安全：163.23.89.65/AP/read17/view17.php?id=1154

* session.use_only_cookies设置为1，避免session固定攻击
* sesison.use_trans_sid设置为0，避免链接传递session id

# sendHeaders 发送相应头

* 设置最终修改时间，避免被浏览器缓存覆盖
* click-jacking protection 目前处于注释状态，未来可能添加

# initConsoleMode 初始化命令行模式

* 当$server['REQUEST_METHOD']为空时，则说明不是通过浏览器访问，开启console模式（定义CONSOLE常量）
* 默认为本地访问，GET请求，客户端为Console

# processRequest 删除$_GLOBAL全局变量，并合并$_POST和$_GET，进行参数安全过滤

* 检测register_globals，如果开启则进行赋值，将原全局变量unset，用局部变量代替

参数过滤参数，防止代码攻击和SQL注入

* 对请求中的所有参数使用stripslashes函数，去除转义反斜杠
* 对请求中的参数key和value使用strip_tag函数，去除HTML和PHP关键字 www.php.net/manual/zh/function.strip-tags.php
