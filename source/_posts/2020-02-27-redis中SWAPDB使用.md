---
layout: photo
title: redis中SWAPDB使用
tags:
  - DB
date: 2020-02-27 23:27:37
categories: DB
photos:
---
工作用遇到redis需要生成新的数据，但是想保留老数据，在不改变代码的情况下，可以使用SWAPDB交换两个数据库内容。
<!--more-->
#### SWAPDB index index
> 起始版本：4.0.0

  该命令可以交换同一Redis服务器上的两个DATABASE，可以实现连接某一数据库的连接立即访问到其他DATABASE的数据。
  访问交换前其他database的连接也可以访问到该DATABASE的数据。
  简单讲解：
   SWAPDB 1 3
   所有访问1号数据库的连接立刻可以访问到3号数据库的数据。
   访问3号数据库的连接立即可以访问1号数据库的数据。

返回值
> SWAPDB执行成功返回OK .

```redis
# 例子
SWAPDB 1 3
```

