---
layout: post
category: docker
title: "docker安装"
tags: docker installation
---

# docker安装
* [https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04)
* [https://docs.docker.com/install/](https://docs.docker.com/install/)

## 系统环境
* Ubuntu 18.04

## 通过官方提供的apt仓库安装

### 准备安装使用的工具
* `sudo apt-get install apt-transport-https ca-certificates curl software-properties-common`

### 添加官方apt仓库
* `curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`
* `sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"`

### 更新本地apt仓库信息
* `sudo apt-get update`

### 查看软件包信息，确认新添加的apt仓库已经生效
* `apt-cache policy docker-ce`
* 结果中如果有新添加的download.docker-com域名，证明已经开始使用新添加的apt仓库

### 安装docker软件包
* `sudo apt-get install docker-ce`

### 查看docker服务状态
* `sudo systemctl status docker`
    * `sudo systemctl start docker`启动docker服务
    * `sudo systemctl stop docker`停止docker服务

## 避免使用sudo
* 由于docker命令需要sudo权限，所以需要`sudo docker`来调用，也可以通过将现有用户加入docker组来避免每次使用都要用sudo
* `sudo usermod -aG docker ${USER}`
* logout当前用户，再重新login即可生效，或者使用下面的命令避免logout
    * `su - ${USER}`
* `id -nG`已经可以看到当前用户的组已经有docker组了

# 使用国内镜像
* 由于众所周知的原因，中国地区连接dockerhub拉取各种image很慢，可以使用国内镜像来加速
* [https://www.docker-cn.com/registry-mirror](https://www.docker-cn.com/registry-mirror)

## 指定镜像
* 创建/etc/docker/daemon.json文件
* 内容如下
```
{
  "registry-mirrors": ["https://registry.docker-cn.com"]
}
```
