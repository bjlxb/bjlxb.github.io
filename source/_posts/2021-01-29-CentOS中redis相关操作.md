---
layout: photo
title: CentOS中redis相关操作
tags:
  - DB
date: 2021-01-29 16:04:34
categories: DB
photos:
---
CentOS中redis的使用
<!--more-->
## 安装redis
```bash
yum install redis
```
## 修改配置文件
为了能让redis在后台启动，需要修改配置文件中一个参数
```bash
vim /etc/redis.conf
# 找到 daemonize 属性
daemonize no
# 将no改为yes
daemonize yes
```
## 后台启动
```bash
redis-server /etc/redis.conf &
```
## 停止redis
```bash
redis-cli shutdown
```
## redis命令合集
```bash
redis执行了make install后，redis的课执行文件都会自动复制到 /usr/local/bin 目录
redis-server        redis服务器
redis-cli            redis命令行客户端
redis-benchmark        redis性能测试工具
redis-check-aof        aof文件修复工具
redis-check-dump    rdb文件检查工具
```

