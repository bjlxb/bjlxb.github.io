---
layout: photo
title: less-loader因为版本导致的问题
tags:
  - 前端
date: 2021-04-20 19:06:09
categories: 前端
photos:
---
升级less-loader后因为版本过高报错！
<!--more-->
#### 报错信息
```
Syntax Error: TypeError: this.getOptions is not a function
```
#### 场景重现
```
npm install -D less-loader less
```
#### 解决方案
1. 卸载 less-loader
```
npm uninstall --save less-loader
```
2. 安装低版本的less-loader
```
npm install -D less-loader@7.3.0
```
经查询资料版本为7.3.0以下目前是没有问题