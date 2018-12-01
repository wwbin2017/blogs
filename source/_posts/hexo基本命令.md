---
title: hexo基本命令
date: 2018-03-23 23:14:09
tags: Hexo
---


## 常见命令

##### 新建博客页，md文件
```shell
$ hexo new [layout] <title>
```

##### 生成静态网页
```shell
$ hexo generate
$ hexo -g
```
选项 | 描述|
- | :-:  
-d，--deploy | 文件生成后立即部署网站
-w， --watch | 监视文件变动

##### 启动服务
server
```shell
$ hexo server
```
启动服务器。默认情况下，访问网址为： http://localhost:4000/。

选项	| 描述
- | :-:
-p, --port	| 重设端口
-s, --static	| 只使用静态文件
-l, --log	| 启动日记记录，使用覆盖记录格式
