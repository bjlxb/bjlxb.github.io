---
layout: photo
title: Mac上Golang的环境配置
tags:
  - Golang
date: 2021-01-04 10:39:18
categories: Golang
photos:
---
记录一下Mac中配置Golang开发环境！
<!--more-->
1.初始环境
Homerbrew 安装参考:http://brew.sh/
2. 安装Golang
```bash
brew install go
```
3. 查看是否安装成功
```bash
go version
```
出现如下证明安装成功：
```bash
go version go1.15 darwin/amd64
```
4. 配置GOPATH
查看go 的环境变量设置的命令
```bash
go env
```
需要设置的环境变量包括:GOPATH ,GOBIN 以及把GOBIN加入到PATH中,GOROOT变量默认已经设置好。

在fishshell设置GOPATH：
最后的路径按照上面的版本号进行对应
```bash
set -gx GOPATH /usr/local/Cellar/go/X.X.X
```
在bash中设置：
vim ~/.bash_profile

```bash
export GOPATH=/usr/local/Cellar/go/1.7.6
export GOBIN=$GOPATH/bin
export PATH=$PATH:$GOBIN
```
使修改立刻生效:
```bash
source ~/.bash_profile
```

