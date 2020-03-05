---
layout: photo
title: PuTTY生成ppk文件并使用ssh私钥登录
tags:
  - Tool
date: 2020-01-29 20:06:29
categories: Tool
photos:
---

PuTTY默认不使用ssh keys免密登录，需要进行配置，简单记录一下步骤！

<!--more-->

#### 1. 生成公钥和私钥

1. 使用puttygen，点击Generate生成ssh公钥和私钥。
<img src="/image/PuTTY/生成ssh公钥私钥.png">
2. 若已有ssh公钥和私钥，选择load按钮，选择需要加载的私钥。
<img src="/image/PuTTY/加载已存在的私钥.png">
3. 生成私钥，保存至指定位置。
<img src="/image/PuTTY/生成私钥.png">

#### 2. PuTTY端配置
1. 打开PuTTY，在Connection-->Data中配置登录用户名
<img src="/image/PuTTY/添加用户名.png">
2. 在Connection-->SSH-->Auth中加载之前保存的*.ppk文件
<img src="/image/PuTTY/选择私钥.png">
<img src="/image/PuTTY/打开私钥.png">
<img src="/image/PuTTY/添加ppk文件.png">
3. 选择Session填写Host Name信息后可以选择直接连接或填写Saved Sessions，点击Save保存该Session
<img src="/image/PuTTY/保存并连接服务器.png">
4. 点击Open，若之前配置没问题，应该可以直接连接上
####  3.配置免密登录

可以查看上一篇文章，链接如下：

[ssh免密登录]( https://bjlxb.github.io/2020/01/29/ssh%E5%85%8D%E5%AF%86%E7%99%BB%E5%BD%95/)


