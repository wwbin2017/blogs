---
title: shell编程每天一点 01
date: 2018-03-23 23:53:09
tags: SHELL编程
---

#### date
显示当前时间

#### 后台运行程序
```shell
source test.sh & #注销会停止
nohup test.sh &   # 退出继续运行
```
#### 定时任务
命令 crontab  
基本格式 :

1 | 2 | 3 | 4 | 5 |6
-  | :-:|:-:|:-:|:-:|:-:|:-:|:-:|
*  | *  |*  |*  |*  |command
分　| 时　| 日　 |月　| 周　| 命令

第1列表示分钟1～59 每分钟用\*或者 \*/1表示

第2列表示小时1～23（0表示0点）

第3列表示日期1～31

第4列表示月份1～12

第5列标识号星期0～6（0表示星期天）

第6列要运行的命令
```shell
$crontab -e # 默认使用vim打开crontab
```
crontab文件的一些例子：
``` shell
#每晚的21:30重启apache。
30 21 * * * /usr/local/etc/rc.d/lighttpd restart
#每月1、10、22日
45 4 1,10,22 * * /usr/local/etc/rc.d/lighttpd restart
#每天早上6点10分
10 6 * * * date
#每两个小时
0 */2 * * * date
#晚上11点到早上8点之间每两个小时，早上8点
0 23-7/2，8 * * * date
#每个月的4号和每个礼拜的礼拜一到礼拜三的早上11点
0 11 4 * mon-wed date
#1月份日早上4点
0 4 1 jan * date
```
