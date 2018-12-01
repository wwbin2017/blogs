---
title: Git使用基础 02
date: 2018-03-27 22:05:39
tags: GitHub基础
---

#### 删除分支
 #### 恢复被删除的分支
 ```shell
 #!/bin/bash
 git branch -d <branch_name>
 ```
 Git会自行负责分支的管理，所以当我们删除一个分支时，Git只是删除了指向相关提交的指针，但该提交对象依然会留在版本库中。

因此，如果我们知道删除分支时的散列值，就可以将某个删除的分支恢复过来。在已知提交的散列值的情况下恢复某个分支：
```shell
#!/bin/bash
git branch <branch_name> <hash_val>
```
可以使用reflog命令找到hash值
