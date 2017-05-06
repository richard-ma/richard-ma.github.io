---
layout: post
category: nginx
title: "nginx负载均衡配置"
tags: nginx load_balancer
---

# nginx负载均衡配置

```
# 这里是后端服务器列表
# 本例设置了两台后端服务器,可根据需要添加或改写,每个服务器列出IP和Port即可
upstream backend { # 这里填写你网站的域名即可
    # 指派服务器策略(这里我使用了ip_hash,因为大多数网站都是动态的)

    ip_hash; # 根据请求的IP地址经过哈希算法得出对应的服务器进行指派,动态网站常用的策略.客户不会因为刷新页面就跳到另一台服务器上,所以客户端刷新时看不出是用了负载均衡,避免了动态网站的Session同步问题,最为常用的策略
    server 192.168.31.199:5000 max_fails=3 fail_timeout=30s;
    server 192.168.31.199:5001 max_fails=3 fail_timeout=30s;
    ###############################################################
    # 服务器参数:
    # max_fails: 允许请求失败的次数.当有3次请求失败时,则认为这台服务器有问题,返回proxy_next_upstream模块定义的错误
    # fail_timeout: 当超过max_fails允许的错误次数后,暂停这台服务器服务的时间.当超过max_fails限制时,10秒内不会给这台服务器分配新的请求(一般配合服务器自动重启机制,这个时间刚好是服务器能自动重启需要的时间),max_fails和fail_timeout一般连用
    # max_conns: 服务器最大接受的请求数.达到设置的数量时将不会给这台服务器继续派发请求,服务器状态视为忙.默认设置为0,当设置为0时表示不限制.
    ###############################################################
    # 其他服务器参数:
    # server 192.168.31.200:80 down; # down: 这台服务器不启用.可能是正在维修的服务器,可以用这种方法手动关闭,这样负载均衡服务器不会给这台派发请求,等故障排除后,删除掉down参数就可以继续投入服务了.
    # server 192.168.31.201:80 backup; # backup: 预留的备份机器. 这台服务器只有当所有一般服务器都故障时或者全忙时才会把请求派发给这台服务器,所以这台服务器压力最轻.

    ###############################################################
    # 其他方案
    ###############################################################
    # 轮询方案1: 按照请求到来的时间按顺序指派服务器,对于纯静态内容适用,浏览器刷新时会跳转到其他服务器,需要加入服务器间的session同步处理
    #server 192.168.31.199:5000;
    #server 192.168.31.199:5001;
    ###############################################################
    # 轮询方案2: 按照请求到来的时间按顺序和weight值指派服务器,对于纯静态内容适用,浏览器刷新时会跳转到其他服务器,需要加入服务器间的session同步处理
    #server 192.168.31.199:5000 weight=3; # 每5次请求给这台服务器分配3次,此服务器压力较大
    #server 192.168.31.199:5001 weight=2; # 每5次请求给这台服务器分配2次,此服务器压力较小
    ###############################################################

    ###############################################################
    # ip_hash还是轮询
    # 从请求派发的压力上看,轮询能让服务器的压力更为平均.如果出现同一局域网多台客户访问时,由于客户来源IP是同一个,所以可能造成使用ip_hash时,某台服务器负载过大的情况.而轮询是按顺序平均分配,所以不会出现服务器负载分布差别巨大的情况.
    # 轮询在处理动态页面时有Session同步问题.比如客户A进行登录操作时被分配到了backend1服务器服务,其登录的Session信息都保存在backend1上;当访问第二个页面时分配到backend2进行服务,需要Session验证登录,而backend2上并没有Session信息,就会造成用户不能正常使用.但如果使用ip_hash就不会有这种情况发生,因为对于同一个客户来说,它始终会被分配到同一台backend服务器上进行操作,不需要同步Session.
    ###############################################################
    # 目前较为流行的解决Session同步和负载均衡压力的方法有两种:
    # 1. 动静分离
    # 将网站代码和静态图片css等文件分离,放到不同的服务器上.对于图片和css,js文件等静态内容使用轮询;对于动态部分使用ip_hash.
    # 2. Session同步
    # 全站使用轮询做负载均衡,在backend服务器之间使用Session同步机制,让每台backend服务器上都能获取到每个在线用户的Session信息.这已经超出了nginx的讨论范围,这里不展开.
    ###############################################################
}

server {
    listen       80; # 端口
    server_name  localhost 192.168.31.199 yourdomain.com; # 这里可以改为网站的域名

    location / {
        proxy_pass http://backend; # 将所有请求交给负载均衡

	proxy_set_header Host $host; # 转发请求
	proxy_set_header X-Real-IP $remote_addr; # 转发客户端IP
	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for; # 转发客户端IP
	
	proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504 http_403 http_404; # backend服务器出现如下问题时都直接返回给下一个负载均衡里的服务器

	# 在负载均衡和backend服务器路径不变的情况下,Cookie是自动转发的,所以不需要设置
    }

    # 生产环境配置负载均衡时还需理解后进行,切不可生搬硬套本配置文件.

    # 以下内容是nginx安装时给出的一些配置例子,不属于负载均衡配置部分.
    # proxy the PHP scripts to Apache listening on 127.0.0.1:80
    #
    #location ~ \.php$ {
    #    proxy_pass   http://127.0.0.1;
    #}

    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    #
    #location ~ \.php$ {
    #    root           html;
    #    fastcgi_pass   127.0.0.1:9000;
    #    fastcgi_index  index.php;
    #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
    #    include        fastcgi_params;
    #}

    # deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    #location ~ /\.ht {
    #    deny  all;
    #}
}

```

# 参考文献
1. [http://nginx.org/en/docs/http/ngx_http_upstream_module.html](http://nginx.org/en/docs/http/ngx_http_upstream_module.html)
1. [https://www.zybuluo.com/phper/note/89391](https://www.zybuluo.com/phper/note/89391)
1. [https://www.zybuluo.com/phper/note/90310](https://www.zybuluo.com/phper/note/90310)
1. [https://www.zybuluo.com/phper/note/133244](https://www.zybuluo.com/phper/note/133244)
1. [http://www.php100.com/html/program/nginx/2013/0905/5525.html](http://www.php100.com/html/program/nginx/2013/0905/5525.html)
