---
title: VSCode安装
date: 2017-11-02 13:41:41
tags: VSCode
mathjax: true
---
环境 ubuntu16.04
打开终端执行以下命令
``` shell
sudo add-apt-repository ppa:ubuntu-desktop/ubuntu-make
sudo apt-get update
sudo apt-get install ubuntu-make
```
安装好之后，运行下面的命令：
```
umake web visual-studio-code  # 有可能网速不好，多试几次就行了
```
要卸载并从 Ubuntu 系统中删除 Visual Studio 代码, 在终端中运行下面的命令:
```
umake web visual-studio-code --remove
sudo apt-get remove ubuntu-make
```
