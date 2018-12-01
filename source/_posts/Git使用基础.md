---
title: Git使用基础
date: 2017-11-02 22:29:41
tags: GitHub基础
---
--------------------------------------------
### git初始设置
#### 设置用户名和邮箱地址
```
git config --global user.name "username"
git config --global user.email "email@email.com"
```
上诉命令会在 "~/.gitconfig"中生成相应的信息，可以直接修改，可以使用任何的用户名和邮箱。
#### 提高可读性设置
```
git config --global color.ui auto
```
这样命令的输出很容易分辨。
#### 设置SSH Key
Github上连接已有的仓库时的认证，是通过ssh的公开密钥认证方式进行的。因此需要创建SSH Key，并且添加到github中。
```
ssh-keygen -t rsa -C "your_email@163.com"
```
在 "~/.ssh"文件中有id_rsa  id_rsa.pub 文件，其中id_rsa.pub是共有密钥。
#### 添加公开密钥
进入 “setting” 点击右 ”Add SSH Key” 输入公开密钥（id_rsa.pub中的内容）。
.gitignore文件把不需要版本管理的文件记录在其中。
#### Git基本命令
```shell
git init # 初始化仓库
git status # 查看仓库的状态
git add # 向暂存区中添加文件
```
#### git commit 保存仓库的历史记录
```
git commit -m “描述性的文字”
```
```
git log # 查看提交日志，当前状态为终点的历史日志
git log --pretty=short # 查看提交日志
git log -p # 显示文件的改动
git log --graph # 以图表的形式查看分支
git relog # 查看操作日志
```
```
git diff # 查看更改后的差别
git diff HEAD # 查看工作树和最新提交的差别
```
#### 分支操作
在进行多个并行任务时，会用到分支。
```
git branch # 显示分支 ，带*表示当前分支
git checkout -b ‘分支名’ #创建分支，并且切换
# 或者
git branch ’分支名’ # 创建分支
git checkout ‘分支名’ # 切换分支
```
#### 合并分支
首先需要切换到master主分支
```
git merge --no-ff '分支名'
```
当发生冲突的时候，需要打开对应的文件，解决冲突。其中冲突文件中“==========”以上是HEAD内容，以下是需要合并的内容。
#### 更改提交的操作
回溯之前的提交
```
git reset --hard ‘提交的hash值’ #
```
```
git commit amend # 修改提交信息
```
