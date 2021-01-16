---
layout: photo
title: ERROR：Public Key Retrieval is not allowed
tags:
  - Java
date: 2019-05-23 23:18:35
categories: Java
photos:
---
Spring+Mybatis项目中连接Mysql数据库报错Public Key Retrieval is not allowed。
<!--more-->
解决方案：
```java
在数据库链接中添加：
jdbc.url = jdbc:mysql://127.0.0.1:3306/${jdbc.dbName}?useUnicode=true&useSSL=false
&allowPublicKeyRetrieval=true
```

