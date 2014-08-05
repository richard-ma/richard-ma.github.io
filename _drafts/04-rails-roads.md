---
layout: post
category: rails
sid: 4
title: "[Date with Rails] Rails之路"
tags: ruby rails
---

# Rails之路

上次我们用rails generate命令生成了一个ActiveRecord，名叫Blog。其实rails generate命令也是可以被懒人写成这样的：

`$ rails g scaffold Blog title:string author:string content:string`

也就是g作为generate的缩写形式。

记得上一篇我说过如果要访问Blog的相关页面需要使用的URL是复数吗？

`http://localhost:3000/blogs`

这里的blogs是Blog的复数形式。如果你接受过中国英语的教育，应该清楚除了+s这种标准形式之外，还有很多不规则变换。非常有节操的我就调戏了一下Rails，创建了一个ActiveRecord叫做Person，当然正确的复数形式应该是People。你也可以这么做，然后访问一下这个URL：

`http://localhost:3000/people`

记得在访问之前让数据库创建表哦！

`$ rake db:migrate`

访问前，还要启动Rails的服务器哦！

`$ rails server`

如果这两样在我说之前都做到了，很好，前面的技能你已经掌握得很熟练了。现在到浏览器中看看那个people的URL结果吧！页面出来的一刹那，你是不是感觉被Rails调戏了？

## Routing

我们先看看Rails为我们生成的页面都有哪些功能，以及对应的URL是怎样的。

|操作                  | URL                        |
|----------------------|----------------------------|
|默认首页（记录列表）  | /blogs                     |
|新建记录表单          | /blogs/new                 |
|创建记录              | /blogs                     |
|显示记录（记录细节）  | /blogs/:id                 |
|编辑记录              | /blogs/:id/edit            |
|修改记录              | /blogs/:id                 |
|删除记录              | /blogs/:id                 |

这些连接可以一一访问，:id代表了记录的id号码，列表中会显示这个项目。细心的你也许会发现很多URL有重复的情况，比如/blogs/:id这样的URL，究竟是要显示记录细节呢？还是要修改记录呢？又或者是要删除记录呢？其实如果直接访问这样的URL，是显示记录细节的，而其他两个功能是无法做到的。

Rails是如何实现相同的URL执行不同的操作呢？其实秘密在于使用了不同的method发送请求。手写过HTML Form的童鞋应该都知道HTTP请求常用的有GET和POST两种：GET是一般的页面访问，POST被用于提交Form信息，原因是Post允许携带的信息比GET要大，所以用GET请求上传文件啥的基本不可能，而POST请求可以做到。

现在流行的Web开发框架都在鼓吹一个概念，支持RESTful的应用。RESTful具体是什么由于超出本系列范围，所以请读者自行Google之。但RESTful的初衷就是让Web应用更加规范化，甚至不同应用之间由于有RESTful的约束变得可以相互调用，实现了RESTful几乎就是对外开放了一套应用的API。

而Rails刚才使用相同URL实现不同操作效果的操作，就是利用了另外两种HTTP协议的请求：PUT和DELETE。这两个请求在很早就有了，不过一直没有被人重视，直到RESTful被提出以后，才广为人知。

这样的话，刚才那个表就要加上一列：发送方法（Method）

|操作                  |URL              |Method|
|----------------------|-----------------|------|
|默认首页（记录列表）  |/blogs           |GET   |
|新建记录表单          |/blogs/new       |GET   |
|创建记录              |/blogs           |POST  |
|显示记录（记录细节）  |/blogs/:id       |GET   |
|编辑记录              |/blogs/:id/edit  |GET   |
|修改记录              |/blogs/:id       |PUT   |
|删除记录              |/blogs/:id       |DELETE|

`/blogs/:id`

对于上面同样一个URL来说，如果用GET方法发送HTTP请求就是显示记录；如果用PUT方法发送就是修改记录；如果用DELETE方法发送就是删除记录。当然:id指明了操作对象，Rails的ActiveRecord都有一列叫做id的Primary Key（PK：主键，详见数据库相关书籍）。

## routes.rb

前面提到在`/config/routes.rb`文件中定义了所有URL和Controller之间的对应关系，而Controller又决定了使用什么样的View。举例来说，比如我们访问了一下`http://localhost:3000/blogs`这个URL，过程如下。

     http://localhost:3000/blogs
       |
       | 向服务器发送一个GET请求，经过Rails匹配，
       | 分配给blogs controller的index方法处理。
       v
     /app/controllers/blogs_controller.rb(index)
       |  
       | blogs controller的index方法默认的view
       | 就是下面这个文件。
       v
     /app/views/blogs/index.html.erb

关于Controller是如何和View部分对应的，我们以后再表。现在清楚了/blogs这个URL对应的Controller方法，其他的URL呢？blogs对应的Controller是`/app/controllers/blogs_controller.rb`文件，所有Controller函数定义都在这个文件里。

|操作                  |URL               |Method        |Controller  |
|----------------------|------------------|--------------|------------|
|默认首页（记录列表）  |/blogs            |GET           |index       |
|新建记录表单          |/blogs/new        |GET           |new         |
|创建记录              |/blogs            |POST          |create      |
|显示记录（记录细节）  |/blogs/:id        |GET           |show        |
|编辑记录              |/blogs/:id/edit   |GET           |edit        |
|修改记录              |/blogs/:id        |PUT           |update      |
|删除记录              |/blogs/:id        |DELETE        |destroy     |
                                                                            
现在操作，URL， Method和Controller中的方法就都对应上了，而这些全部都是Rails自动完成的，在`/config/routes.rb`文件中只有一句配置：

`resources :blogs`

而这句在执行rails generate时候Rails也帮你写入到`/config/routes.rb`中去了，所以你几乎什么都不用做。

## 总结

今天弄清楚了Rails的URL和Controller中的函数对应关系，基本就可以知道整个Rails应用的程序执行走向了。但我们还有一个部分不是很清楚，就是View（视图）部分，下一篇就说这个，休息一下。
