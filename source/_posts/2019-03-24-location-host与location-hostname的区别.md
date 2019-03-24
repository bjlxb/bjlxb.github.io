---
layout: photo
title: location.host与location.hostname的区别
tags:
  - JavaScript
date: 2019-03-24 23:19:04
categories: JavaScript
photos:
---
Django项目中使用到了验证码库，需要用AJax调用刷新，请求固定的URL
<!--more-->

| 属性     | 值                  |
| :------- | :------------------ |
| href     | 完整的 URL          |
| protocol | 协议                |
| hostname | 主机名              |
| host     | 主机名加端口号      |
| port     | 的端口号            |
| pathname | 当前 URL 的路径部分 |
| search   | URL 的查询部分      |
| hash     | #开始的锚           |

--------------------------------------------------------------------------------

## 区别：
- location.host 
包含端口，比如是 127.0.0.1:81。如果端口是 80，那么就没有端口，就是 127.0.0.1。
- location.hostname 
不包含端口，比如是 127.0.0.1。

--------------------------------------------------------------------------------
- Location port
port 属性是一个可读可写的字符串，可设置或返回当前**URL 的端口部分**。
注意：如果端口号就是80（这是默认的端口号)，无需指定。
语法
	location.port
	
--------------------------------------------------------------------------------

- Location protocol 
protocol 属性是一个可读可写的字符串，可设置或返回当前** URL 的协议**。
语法
	location.protocol