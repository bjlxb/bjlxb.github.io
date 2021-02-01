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
## redis命令行客户端
```bash
# 1. 发送命令
redis-cli shutdown
# 2. 交互模式，默认是127.0.0.1和6379端口,只要使用这种模式！
redis-cli -h 127.0.0.1 -p 6379
# 命令返回值
127.0.0.1:6379> ping
PONG #表示可用
```
## 错误解决
1. 错误信息：
MISCONF Redis is configured to save RDB snapshots, but is currently not able to persist on disk. Commands that may modify the data set are disabled. Please check Redis logs for details about the error.
Redis被配置为保存数据库快照，但它目前不能持久化到硬盘。用来修改集合数据的命令不能用。请查看Redis日志的详细错误信息。
2. 原因
强制关闭Redis快照导致不能持久化。
3. 解决方案
在服务器将stop-writes-on-bgsave-error设置为no
```bash
127.0.0.1:6379> config set stop-writes-on-bgsave-error no
```
[参考链接](https://www.jianshu.com/p/3aaf21dd34d6)