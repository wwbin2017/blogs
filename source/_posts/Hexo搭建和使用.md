---
title: Hexo搭建和使用
date: 2017-10-30 21:24:23
tags: Hexo
---
主要简单介绍在ubuntu环境下Hexo的搭建以及一些常用配置和命令的使用
### hexo环境搭建和使用
##### hexo环境搭建
* 主要参考 [Hexo官方文档](https://hexo.io/) [中文文档](https://hexo.io/zh-cn/docs/)总结
* 首先需要安装git和Node.js
* 安装git
```
    Windows：下载并安装 git.
    Mac：使用 Homebrew, MacPorts ：brew install git;或下载 安装程序 安装。
    Linux (Ubuntu, Debian)：sudo apt-get install git-core
    Linux (Fedora, Red Hat, CentOS)：sudo yum install git-core
```
* 安装Node.js
```
安装 Node.js 的最佳方式是使用 nvm。
cURL:
$ curl https://raw.github.com/creationix/nvm/master/install.sh | sh
Wget:
$ wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh
安装完成后， 重启终端 并执行下列命令即可安装 Node.js。
$ nvm install stable
```
* 安装好上述环境后，就可以安装Hexo
```
$ npm install -g hexo-cli  不要加sudo
```
* 为了部署到github需要安装一个扩展
```
$ npm install hexo-deployer-git --save
```

* 有时候需要改变用户名和邮箱
```
设置你的用户名
git config --global user.name "user_name"  
设置你的邮箱
git config --global user.email "email@gmail.com"
```
### hexo使用
