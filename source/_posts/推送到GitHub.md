---
title: 推送到GitHub
date: 2017-11-03 22:58:33
tags: GitHub基础
---

---------------------------------------------------------
#### 添加远程仓库
```
git remote add origin git@github.com:用户名/仓库名.git
```
#### 推送远程仓库
```
git push -u origin master
```
推送其他分支
```
git checkout -b feature-A
git push -u origin feature-A
```
#### 从远程仓库获取
```
git clone git@github.ccom:用户名/仓库名.git
git checkout -b feature-A origin/feature-A
```
#### 获取最新的远程仓库分支
```
git pull origin feature-A
```
