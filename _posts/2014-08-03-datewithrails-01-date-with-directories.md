---
layout: post
category: rails
title: [Date with Rails] 目录的约定
tags: ruby rails
---

# 目录的约定

## 创建新应用

在Rails安装完毕后，创建一个应用十分容易，只需要一个命令就可以搞定。

`$ rails new my_app`

注：my_app可以替换成你应用的名称

Rails如果想顺利运行，首先就要能找到各种文件，所以要先了解一下Rails对于目录结构的约定。

## 目录树

进入my_app目录，使用如下命令

`$ cd my_app`

进入my_app目录，我们会看到rails究竟为我们的下一步开发做了哪些准备工作。由于后续工作基本就在my_app目录中进行，为了节省篇幅和打字时间，我将这个目录以后就称为应用目录，写成/。

首先是几个独立的文件

* /
* config.ru 对于rake提供的Webserver进行配置，初学者不用修改
* Rakefile 定义rake的task，初学者不用修改
* README.rdoc Rails的简单文档说明，至今没改过，仍那仍着吧
* Gemfile Gem包配置文件，如果想安装某个Gem包可以将名字写在这里
* Gemfile.lock Gem包状态，用来记录当前安装了哪些Gem包。Gem系统负责管理这个文件，一般不用人为修改和维护。

这里提到了Gem，Gem是ruby自己的包管理系统。类似Linux的许多发行版包管理：rpm, apt, pacman等等，Gem对于Rails模块代码的重用起着关键的作用。Rails将许多常用功能封装为Gem包，使用者想使用时只要用Gem安装一下便可以直接在框架内使用了。

然后就是一些目录了，我把他们都列出来

* /
* app 这个目录存放应用的MVC文件
* config 很明显，对应用的配置和数据库连接参数
* db 对数据库的管理文件
* doc 应用文档
* lib 不属于MVC的文件一般放到这里（这个目录默认是不启用的）
* log 日志存放处
* public 直接访问的静态文件，如404页面和默认的首页等
* script Rails工具脚本
* test 各种测试需要的文件，敏捷开发的测试编写是十分重要的
* tmp 运行是产生的临时文件（不需要人为维护）
* vendor 导入的一些代码（扩展Rails的plugins或者将Gem包都装到这里）

由于Rails最关心的就是MVC部分的开发，所以app目录中的文件应该是最常用的了。所谓MVC开发就是将应用分解为三个部分：模型(model)，视图(view)，控制器(controller)：

* 模型主要是跟数据库打交道，比如常用的内容管理系统（CMS）中的文章就是一个model
* 控制器是主要的应用逻辑代码产生的地方，它负责从用户操作或model中读取数据，处理数据，然后用变量的形式传递给视图
* 视图的任务就是展示数据。例如一个表格，视图决定是用HTML展示成网页，还是形成一个PDF文件让用户下载

app目录下的结构如下 

* /app
* assert 各种图片, CSS, Javascript文件
* controllers 控制器C部分
* helpers helper至今不知道怎么翻译，就是方便开发的一些函数写在这里
* mailers 邮件相关文件，Rails默认是支持邮件发送的，但需要单独配置邮件服务器
* models 模型M部分
* views 视图V部分

## Rails Run！

了解了基本的目录结构，现在应该让Rails跑起来了。如果你的计算机暂时没有nginx或者apache，甚至是Windows下没有IIS，都没有关系。Rails自带了一个web server，绝对能满足开发需求。

`$ rails server`

这样就可以开启这个web server了。现在打开浏览器输入 `http://localhost:3000` 如果能看到Rails的欢迎页面，那证明Rails就运行了。不过这里并没有用到先前提到的MVC那么复杂的部分，显示的只是/public/index.html这个静态文件。

悄悄告诉你有个偷懒的写法：

`$ rails s`

很明显s是server的缩写。

## 总结

现在让rails第一次运行的感觉是不是很好呢？每次学会一种新事物时，当它告诉你I'm working!总是有成就感的。为了让rails带给你更大的惊喜，我首先要唠叨一下应用的配置。俗话说磨刀不误砍柴工。工欲善其事，必先利其器！下一篇就唠叨一些Rails配置的约定。
