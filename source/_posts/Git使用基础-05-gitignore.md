---
title: Git使用基础 05 gitignore
date: 2018-03-27 22:37:21
tags: GitHub基础
---

#### 忽略文件原则
忽略操作系统自动生成的文件，比如缩略图等；
忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；
忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。

#### 语法规范
* 空行或是以#开头的行即注释行将被忽略；
* 以斜杠 “/” 结尾表示目录；
* 以星号 “\*” 通配多个字符；
* 以问号 “?” 通配单个字符
* 以方括号 “[]” 包含单个字符的匹配列表；
* 以叹号 “!” 表示不忽略(跟踪)匹配到的文件或目录；
* 可以在前面添加斜杠 “/” 来避免递归,下面的例子中可以很明白的看出来与下一条的区别。

.gitignore分为全局配置和局部配置

##### python中的例子
\*.py[cod]
*$py.class  
\# C extensions  
\*.so    
\# Distribution / packaging   
.Python      
build/          
develop-eggs/           
dist/             
downloads/            
eggs/             
.eggs/             
lib/              
lib64/             
parts/              
sdist/            
var/              
wheels/                
\*.egg-info/             
.installed.cfg      
\*.egg       
