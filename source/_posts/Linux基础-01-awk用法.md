---
title: Linux基础 01 awk用法
date: 2018-04-03 21:57:57
tags: Linux
---

#### awk基本用法

变量名 | 意义
- | :-: |
$0	| 当前记录（作为单个变量）
$1~$n	| 当前记录的第n个字段，字段间由FS分隔
FS	| 输入字段分隔符 默认是空格
NF	| 当前记录中的字段个数，就是有多少列
NR	| 已经读出的记录数，就是行号，从1开始
RS	| 输入的记录他隔符默 认为换行符
OFS |	输出字段分隔符 默认也是空格
ORS	| 输出的记录分隔符，默认为换行符
ARGC	| 命令行参数个数
ARGV	| 命令行参数数组
FILENAME	| 当前输入文件的名字  *得注意别重名了*
IGNORECASE	| 如果为真，则进行忽略大小写的匹配
ARGIND	| 当前被处理文件的ARGV标志符
CONVFMT	| 数字转换格式 %.6g
ENVIRON	| UNIX环境变量
ERRNO	| UNIX系统错误消息
FIELDWIDTHS	| 输入字段宽度的空白分隔字符串
FNR	| 当前记录数
OFMT	| 数字的输出格式 %.6g
RSTART	| 被匹配函数匹配的字符串首
RLENGTH	| 被匹配函数匹配的字符串长度
SUBSEP	 | \\034

在awk中调用系统变量必须用单引号，如果是双引号，则表示字符串
```shell
str=abcd
awk '{print '$str'}'   # 结果为abcd
awk '{print  "$str"}'   # 结果为$Flag
```

'hllo world'

awk获取外部变量，直接引用不行
```shell
test='awk code'
echo | awk '{print test}' test="$test"
echo | awk -v test="$test" '{print test}'
```

awk 流程控制语句（if,for,while,do)详细介绍

```shell
#!/bin/bash
awk 'BEGIN{
test=100;
if(test>90)
{
    print "very good";
}
else if(test>60)
{
    print "good";
}
else
{
    print "no pass";
}
}'

awk 'BEGIN{
test=100;
total=0;
while(i<=test)
{
    total+=i;
    i++;
}
print total;
}'

awk 'BEGIN{
for(k in ENVIRON)
{
    print k"="ENVIRON[k];
}
}'

```

[awk 内置函数](http://www.cnblogs.com/chengmo/archive/2010/10/08/1845913.html)


#### awk数组
awk其实更像是一个字典类型，因为其下标可以是数字也可以是字符串

[awk 数组](http://www.cnblogs.com/chengmo/archive/2010/10/08/1846190.html)

判断键值存在以及删除键值：
```shell
awk 'BEGIN{tB["a"]="a1";tB["b"]="b1";
if( "c" in tB){print "ok";};
for(k in tB){print k,tB[k];}}'  

awk 'BEGIN{tB["a"]="a1";tB["b"]="b1";
delete tB["a"];for(k in tB){print k,tB[k];}}'                     
```
if(key in array) 通过这种方法判断数组中是否包含”key”键值。

delete array[key]可以删除，对应数组key的，序列值。
