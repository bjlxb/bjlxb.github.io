---
layout: photo
title: Python中datetime格式化
tags:
  - Python
date: 2020-09-08 22:55:31
categories: Python
photos:
---
记录一下Python中datetime的使用。
<!--more-->
**获取当前时间**
```python
import time

#获取今天的字符串
today = time.strftime("%Y-%m-%d",time.localtime(time.time()))
print(today)
```
**当前日期时间**
```python
import datetime

print datetime.datetime.now()
# 2020-09-08 23:20:21.202000

# 格式化时间
import datetime

print datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
# 2020-09-08 23:20:21
```
**多加一天**
```python
import datetime

print (datetime.datetime.now()+datetime.timedelta(days=1)).strftime("%Y-%m-%d %H:%M:%S")
# 2020-09-11 23:16:27
```
**减少一天**
```python
import datetime

print (datetime.datetime.now()+datetime.timedelta(days=-1)).strftime("%Y-%m-%d %H:%M:%S")
# 2020-09-09 23:17:07
```
**减一小时**

```python
import datetime

print (datetime.datetime.now()+datetime.timedelta(hours=-1)).strftime("%Y-%m-%d %H:%M:%S")
# 2020-09-10 22:18:56
```
**减五分钟**

```python
import datetime

print (datetime.datetime.now()+datetime.timedelta(minutes=-5)).strftime("%Y-%m-%d %H:%M:%S")
# 2020-09-10 23:13:23
```
