---
title: redis 操作
date: 2018-07-14 21:43:36
tags: redis
---

## redis 基础操作

```shell
redis-cli -h host -p port -a password
# 密码  
redis 127.0.0.1:6379> auth password
```

基本命令  
> COMMAND KEY\_NAME

数据类型  
Redis支持五种数据类型：string（字符串），hash（哈希），list（列表），set（集合）及zset(sorted set：有序集合)。
