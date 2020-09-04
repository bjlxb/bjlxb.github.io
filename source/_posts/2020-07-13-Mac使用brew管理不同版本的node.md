---
layout: photo
title: Mac使用brew管理不同版本的node
tags:
  - Other
date: 2020-07-13 22:30:15
categories: Other
photos:
---
在使用hexo做博客时，出现nodejs版本过高，无法同步到github的情况，需要切换nodejs版本，记录下mac下切换过程！
<!--more-->
#### 1. 查看当前可用版本
```basic
brew search node
```
后面打勾的表示已安装node版本。
<img src="/image/Node/Node-1.png">
#### 2. 安装指定版本
```basic
brew install node@12
# 若要安装12.x最新版本
brew install node12-lts
```
#### 3. 切换到指定版本
取消当前版本
```basic
brew unlink node
```
切换到指定版本
```basic
brew link node@12
```
一行命令完成上面内容
```basic
brew unlink node && brew link --force node@12
```
#### 4. 查看当前版本
```basic
node -v
```

