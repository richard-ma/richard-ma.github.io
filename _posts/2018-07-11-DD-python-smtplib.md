---
layout: post
category: developing_diaries
title: "[jack-jack]D-Day之Python smtplib"
tags: Python smtplib
---

# [jack-jack]D-Day之Python smtplib

## jack-jack

jack-jack是一个多线程的邮件群发工具，今天开了新坑，准备暑假期间做个雏形出来。

## smtplib

### smtp协议的三种传输方式
* 明文传输： 传统的SMTP协议都是明文传输邮件信息及其内容的，一般使用25端口
* SSL加密： 后来在SMTP协议加上了SSL传输，邮件信息和内容用SSL加密后进行传输，一般使用465端口
* TLS加密： 被认为是更加安全的加密方式，使用TLS对邮件信息和内容进行加密，一般使用587端口。

### smtplib的实现方法
这三种传输方式的实现区别在于调用生成不同的SMTP对象

* 25端口的明文传输（最标准的教科书版本）
```
smtpObj = smtplib.SMTP(server, port) # port default value: 25
```

* 465端口的SSL加密传输（这里用了SMTP_SSL类）
```
smtpObj = smtplib.SMTP_SSL(server, port) # port default value: 465
```

* 587端口的TLS加密传输（这里用了SMTP类）
```
smtpObj = smtplib.SMTP(server, 587) # port = 587 to use TLS
smtpObj.ehlo() # send EHLO command to server
smtpObj.starttls() # send STARTTLS command to server
# enable TLS
```

## Q & A
* Q: QQ邮箱用邮箱密码无法登陆
    * A: 如果使用了授权码，一定要用授权码登陆，用邮箱的密码是无效的。
