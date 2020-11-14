---
layout: photo
title: PowerShell提示无法加载文件
tags:
  - Tool
date: 2020-09-05 20:32:36
categories: Tool
photos:
---
记录下PowerShell提示无法加载文件的解决方案！
<!--more-->

1. 以管理员身份运行PowerShell

2. 执行：get-ExecutionPolicy，回复Restricted，表示状态是禁止的

3. 执行：set-ExecutionPolicy RemoteSigned即可

注：
  以管理员的身份运行PowerShell，而不是cmd窗口！

