---
layout: photo
title: 'Error: The following directories are not writable by your user'
tags:
  - Other
date: 2019-04-11 22:41:19
categories: Other
photos:
---
使用Homebrew安装应用安装应用出现 'Error: The following directories are not writable by your user'错误.
<!--more-->
### Homebrew安装应用报权限错误
```bash
Error: The following directories are not writable by your user:
/usr/local/sbin
You should change the ownership of these directories to your user.
  sudo chown -R $(whoami) /usr/local/sbin

And make sure that your user has write permission.
  chmod u+w /usr/local/sbin
```
### 解决方案
```bash
# 网上方案,未奏效
sudo chown -R 'whoami':admin /usr/local/bin
sudo chown -R 'whoami':admin /usr/local/share
# 解决方案
sudo chown -R $(whoami) /usr/local/sbin
chmod u+w /usr/local/sbin
  
```
