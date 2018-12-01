---
title: Git使用基础 03 之标签
date: 2018-03-27 22:11:52
tags: GitHub基础
---

#### 查看标签
```shell
git tag
git tag -l 'v1.4.2.*' # 查看特定的标签
```

#### 新建标签
```shell
git tag -a v1.4 -m 'my version 1.0'
```

#### 查看标签具体信息
 ```shell
 git show 版本
 ```

#### 分享标签
 默认情况下，git push 并不会把标签传送到远端服务器上，只有通过显式命令才能分享标签到远端仓库。其命令格式如同推送分支，运行 git push origin [tagname] 即可：
```
 $ git push origin v1.5
 ```
 如果要一次推送所有本地新增的标签上去，可以使用 --tags 选项：
```
$ git push origin --tags
```
#### 删除标签
```
$ git tag -d v1.0
```
