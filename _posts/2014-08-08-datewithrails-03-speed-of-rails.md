---
layout: post
category: rails
sid: 3
title: "[Date with Rails] Rails速度"
tags: ruby rails
---

# Rails速度

这里的Blog并不是功能很完善的，如果你愿意，可以作为一个Blog。但它还缺少很多功能，现阶段只能做简单的CRUD操作

## Step1 生成Blog

`$ rails generate scaffold Blog title:string author:string content:string`

这样，Rails会为你生成所有需要的代码。这个命令实际上是让Rails自动生成一个MVC的体系，Controller，Model和View都是以Blog命名的。

这些代码其实是分成几个部分分别生成的，我们来看一看。

第一部分叫active_record，主要是Model部分代码

* /db/migrate/xxxxxx_create_blogs.rb 创建Blog对应的数据库表
* /app/models/blog.rb Blog类
* /test/unit/blog_test.rb 对Blog类的单元测试
* /test/fixtures/blogs.yml 测试用数据

第二部分是Route

* resources :blogs 在/config/routes.rb中添加访问Blog相关页面的URL

第三部分是scaffold_controller，主要是Controller和View部分代码

* /app/controllers/blogs_controller.rb
* /app/views/blogs
* /app/views/blogs/index.html.erb
* /app/views/blogs/edit.html.erb
* /app/views/blogs/show.html.erb
* /app/views/blogs/new.html.erb
* /app/views/blogs/_form.html.erb
* /test/functional/blogs_controller_test.rb
* /app/helpers/blogs_helper.rb
* /app/unit/helpers/blogs_helper_test.rb

第四部分是最后一个部分assets，主要是Javascript和CSS等静态文件

* /app/assets/javascripts/blogs.js.coffee
* /app/assets/stylesheets/blogs.css.scss

coffeescript 和 scss 分别是对Javascript和CSS两中扩展的语法，为的是方便程序员进行写作，但他们不会被浏览器识别，需要编译为真正的Javascript 和 CSS 文件。当然这个编译过程在development环境下是Rails自动完成；而product环境下是在应用初始化时由Rails编译完成放入cache的，为了省去每次访问编译所消耗的时间。

## Step2 数据库是单独处理的

虽然上面生成了所有的代码，但是这个Blog还不能用，因为数据库中还没有对应的表。

`$ rake db:migrate`

使用此命令后，rake会根据上述/db/migrate/xxxxxx_create_blogs.rb中的数据，以及上一篇中提到的/config/database.yml中的设置连接数据库并生成存储数据的结构。

rake在Rails中是数据库的管家，当你需要对数据库进行一些操作的时候，首先看看rake的手册是否已经提供了这些功能。使用rake的好处就是不用去挨个熟悉DBMS中各种“独特的”SQL语法，rake对它们处理得都很好。

## Step3 找到Blog入口

现在启动Rails服务器，访问前面提到过的URL

`http://localhost:3000`

为什么没有变化呢？还是老样子：Rails欢迎你的使用。

我前面提到过了，这个默认的首页是位于/public/index.html文件，所以应用首页并没有变化，因为我们没有改变URL和页面的对应关系（route）。

如果想看看刚才的劳动成果，可以这样写：

`http://localhost:3000/blogs`

注意是复数blogs哦！然后你的Blog就可以使用了。

## 外传：能进能退乃真正Rails

想Blog这样的东西，在Rails中叫做ActiveRecord。如果我们在敏捷迭代开发过程中不小心添加了一个ActiveRecord，那么我们也可以让Rails删除它。

`$ rails destroy Blog`

这样Rails会清除所有的相关文件。但还是刚才的问题，数据库需要单独去处理。但我现在还不清楚rake是否有这样的功能，如果哪位读者找到了清除方法，可以来信或留言告诉我。

## 总结 

今天研习了ActiveRecord在Rails中的使用方法，下一篇我们要深入rails生成的代码中，去看一看那些Rails自动生成的连接和页面跳转的规律。
