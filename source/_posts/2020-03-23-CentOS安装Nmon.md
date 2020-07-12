---
layout: photo
title: CentOS安装Nmon
tags:
  - 测试
date: 2020-03-23 21:48:29
categories: 测试
photos:
---
Nmon是IBM提供的免费的在AIX与各种Linux操作系统上广泛使用的监控与分析工具。
<!--more-->
Nmon 工具是 IBM 提供的免费的在AIX与各种Linux操作系统上广泛使用的监控与分析工具。
该工具可将服务器的系统资源耗用情况收集起来并输出一个特定的文件,并可利用 excel 分析工具nmonanalyser进行数据的统计分析。
nmon运行不会占用过多的系统资源，通常情况下CPU利用率不会超过2%。
#### Centos安装Nmon
```bash
yum -y install nmon
```
#### Nmon直接使用

1. 终端直接输入nmon进入界面，界面如下：
<img src="/image/Nmon/Nmon-1.png">
2. 根据界面提示使用相应命令
```
q : 停止并退出 Nmon
h : 查看帮助
c : 查看 CPU 统计数据
m : 查看内存统计数据
d : 查看硬盘统计数据
k : 查看内核统计数据
n : 查看网络统计数据
N : 查看 NFS 统计数据
j : 查看文件系统统计数据
t : 查看高耗进程
V : 查看虚拟内存统计数据
v : 详细模式
```

#### Nmon生成.nmon报告命令
参数解析：
```
-f 参数:生成文件,文件名=主机名+当前时间.nmon
-T 参数:显示资源占有率较高的进程
-s 参数:-s 10表示每隔10秒采集一次数据
-c 参数:-c 10表示总共采集十次数据
-m 参数:指定文件保存目录
```
命令如下：
```bash
# 每5秒采集一次，共采集12次，实际采集1分钟的数据。
nmon -f -s 5 -c 12 -m /home/lxb/
```

中途需要关闭Nmon，需获取Nmon对应的pid：

```bash
[root@ecs ~]# nmon -f -s 5 -c 12 -m /root/
[root@ecs ~]# ps -ef | grep nmon
root     10747     1  0 21:06 pts/0    00:00:00 nmon -f -s 5 -c 12 -m /root/
root     10840 10511  0 21:06 pts/0    00:00:00 grep --color=auto nmon
[root@ecs ~]# kill -9 10747
[root@ecs ~]# ps -ef | grep nmon
root     10850 10511  0 21:06 pts/0    00:00:00 grep --color=auto nmon
[root@ecs ~]#
```

#### 数据分析

##### 一、使用**nmon analyser**生成图标

1. 下载**nmon analyser**

nmon analyser可以把nmon采集的数据生成直观的Excel表，nmon analyser下载网址：

http://nmon.sourceforge.net/pmwiki.php?n=Site.Nmon-Analyser

<img src="/image/Nmon/Nmon-2.png">

2. **打开nmon analyser**

<img src="/image/Nmon/Nmon-3.png">

 **注：**因为我用的个人免费版WPS（10.1），没有包含宏，需要安装宏插件(VBA for WPS)，Excel是自带宏插件的，如果宏不能运行，需要做以下操作：
工具 -> 宏 -> 安全性 -> 中，然后再打开文件并允许运行宏。

3. **下载VBA for WPS**

地址：https://pan.baidu.com/s/1QzW4ebQxYQtxgVfkTmxVJw，下载VBA7.0.1590_For WPS(中文).exe后，先退出WPS，再直接安装就行，再次打开nmon analyser，启用宏。

4. **使用nmon analyser生成图表**

成功打开nmon analyser后，点击Analyze nmon data按钮，选择nmon数据文件，会再次提示另存为，选择地址保存即可。 

##### 二、在服务器生成html图表

1. 下载生成htnl图表工具：

http://nmon.sourceforge.net/pmwiki.php?n=Site.Nmonchart

2. 解压文件，并进入目录下

3. 修改nmonchart权限
```bash
nmonchart /home/lxb/data/npudev-bigshow-txygz4-179_200325_1819.nmon  /home/lxb/data/npudev-bigshow-txygz4-179_200325_1819.html
```
第一次使用会报错：
```bash
-bash: ./nmonchart: /usr/bin/ksh: bad interpreter: No such file or directory
```
解决方案：
```bash
yum install ksh
```

4. 将html打开，查看数据。