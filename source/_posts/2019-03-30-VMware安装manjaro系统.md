---
layout: photo
title: VMware安装manjaro系统
tags:
  - Other
date: 2019-03-30 23:12:06
categories: Other
photos:
---
周末折腾安装manjaro系统,折腾了一天,踩了许多坑,记录一下!
<!--more-->

## 安装Manjaro

### 下载

官方网站：<https://manjaro.org/get-manjaro/>
目前官方最新版本为18.10，支持都包括xfce,kde,gnome三种桌面环境，选择喜欢的下载，我安装的是xfce桌面。

### 制作U盘启动

使用[Rufus](http://rufus.akeo.ie/)以DD方式写入到U盘，注意此操作会擦除U盘所有数据，请做好备份。
Rufus官方下载：<https://github.com/pbatard/rufus/releases/download/v3.5/rufus-3.5.exe>

## 配置

### 更换软件源

命令行中执行如下命令:

```bash
sudo pacman-mirrors -c China -g  //刷新软件源，会自动选择最快的源
sudo pacman -Syyu  //更新系统
```

编辑文件：`/etc/pacman.d/mirrorlist`,在最上面添加：

```
# 阿里云
Server = http://mirrors.aliyun.com/archlinux/$repo/os/$arch
# 清华大学
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinux/$repo/os/$arch
```

### 添加archlinuxcn软件源

编辑文件`/etc/pacman.conf`，在最下面添加：

```
[archlinuxcn]
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
```



### 更新软件源并导入公钥

```bash
sudo pacman -Syy
sudo pacman -S archlinuxcn-keyring
```

### 更新系统

运行命令：`sudo pacman -Syyu`
出现无法安装更新的问题：`无法安装更新，xxx被manjaro-release所有`解决:
卸载`manjaro-release`:`sudo pacman -R manjaro-release`,再执行更新命令。

### 时区问题
安装完成后,会发现时间总是比实际快了8个小时，试了很多方法，最终使用openNTPD方法解决了问题。
步骤:
```bash
# 安装openNTPD：
sudo pacman -S openntpd
# 重启openNTPD：
systemctl restart openntpd
# 设置开机启动：
systemctl enable openntpd
```
### 垃圾清理
```bash
# 清除系统中无用的包
sudo pacman -R $(pacman -Qdtq)
# 清除已下载的安装包
sudo pacman -Scc
```
