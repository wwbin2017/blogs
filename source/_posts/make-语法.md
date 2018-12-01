---
title: make 语法
date: 2018-07-14 21:43:36
tags: c++编译
---
#### makefile简要语法
基本语法   
target ... : prerequisites ...  
command

* target也就是一个目标文件，可以是Object File，也可以是执行文件。还可以是一个标签（Label）。
* prerequisites就是，要生成那个target所需要的文件或是目标。   
* command也就是make需要执行的命令。（任意的Shell命令）

这是一个文件的依赖关系，也就是说，target这一个或多个的目标文件依赖于prerequisites中的文件，其生成规则定义在command中。说白一点就是说，prerequisites中如果有一个以上的文件比target文件要新的话，command所定义的命令就会被执行。这就是Makefile的规则。也就是Makefile中最核心的内容。

[Makefile](https://www.cnblogs.com/mfryf/p/3305778.html)
