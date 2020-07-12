---
layout: photo
title: JMeter修改ServerAgent的默认端口号
tags:
  - 测试
date: 2020-03-23 21:27:11
categories: 测试
photos:
---
Linux服务器中修改ServerAgent的默认端口号！
<!--more-->
在Linux服务器中，ServerAgent默认启动4444端口，可能会遇到端口占用的情况，需要对端口进行修改，记录一下修改方式！
```bash
# 进入ServerAgent目录中，直接运行命令
java -jar ./CMDRunner.jar --tool PerfMonAgent --udp-port 端口号 --tcp-port 端口号
# 修改启动文件
# 修改startAgent.sh文件如下内容
# java -jar $(dirname $0)/CMDRunner.jar --tool PerfMonAgent "$@"
java -jar ./CMDRunner.jar --tool PerfMonAgent --udp-port 端口号 --tcp-port 端口号
# 后台运行命令
nohup sh startAgent.sh &
```
验证服务外部是否可以访问
```powershell
telent host port
```
