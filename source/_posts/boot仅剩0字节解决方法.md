---
title: boot仅剩0字节解决方法
date: 2017-11-06 19:16:46
tags: Linux
---
当boot存储空间不够时，是因为之前的linux内核还在boot中，因此需要删除旧的内核。首先查看当前linux内核版本，留下当前的版本其他的删除就行
```shell
uname -a
```
查看当强有哪些linux内核版本
```shell
sudo dpkg --get-selections |grep linux-image
```
删除对应的版本，例如 linux-image-4.4.0-78-generic
```shell
sudo apt-get purge linux-image-4.4.0-78-generic
```
查看boot空间大小
```shell
df
```
