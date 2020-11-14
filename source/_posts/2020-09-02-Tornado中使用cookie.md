---
layout: photo
title: Tornado中使用cookie
tags:
  - Django
date: 2020-09-02 20:15:49
categories: Django
photos:
---
记录下Tornado中cookie的使用
<!--more-->
## 一、普通cookie
#### 1. 创建cookie
```python
self.set_cookie(name, value, domain=None,expires=None, path="/", expires_days=None, **kwargs)
```

参数详解：

| 参数名       | 意义                                                         |
| :----------- | :----------------------------------------------------------- |
| name         | 创建cookie的名称                                             |
| value        | 创建cookie的值                                               |
| domain       | 提交cookie时匹配的域名                                       |
| path         | 提交cookie时匹配的路径                                       |
| expires      | cookie的有效期,可以是时间戳整数,时间元组,datetime类型.为UTC时间 |
| expires_days | cookie的有效期天数.优先级低于expires                         |
案例：
```python
class PCookieHandler(RequestHandler):
    def get(self):
        self.set_cookie("name", "kainhuck")
        self.write("ok")

```
#### 2. 原理
设置cookie的原理实际上是通过设置headers中的Set-Cookie来实现的。
```python
self.set_header("Set-Cookie", "name=kainhuck; Path=/")
```
#### 3. 获取cookie
```python
self.get_cookie(name, default=None)
```
参数解释：

| 参数    | 意义                                             |
| :------ | :----------------------------------------------- |
| name    | 要获取的cookie的名称                             |
| default | 如果要获取的cookie值不存在,则返回default的值 |

示例：
```python
class GetComCookie(RequestHandler):
    def get(self):
        cookie = self.get_cookie("name", "NULL")
        print("cookie:",cookie)
        self.write("ok")

```
#### 4. 清除cookie
共有两种方案
**方法一：**

```python
self.clear_cookie(name, path="/", domain=None)
```
删除名为name,并同时匹配domain和path的cookie
**方法二：**

```python
self.clear_all_cookies(path="/", domain=None)
```
删除同时匹配path和domain的所有cookie
示例：

```python
class ClearPCookieHandler(RequestHandler):
    def get(self, *args, **kwargs):
        # 清除一个cookie
        # self.clear_cookie("hello")
        # 清除所有cookie
        self.clear_all_cookies()
        self.write("ok")
```
## 二、安全cookie
tornado提供了一种对cookie进行简易加密方式来防止Cookie被恶意篡改
#### 1.设置安全cookie
设置安全cookie需要一个进行混淆加密的秘钥
例：生成秘钥的方法
```python
import base64
import uuid
key = base64.b64encode(uuid.uuid4().bytes + uuid.uuid4().bytes)
# zmxgH4FZrSHWgtRtbjMnWSP7U8E+P/0Llu5ihRmWbGM4=
```
在tornado.web.Application里添加cookie_secret
```python
"cookie_secret": "zadJa2GJTOu5wGL62RngnVrUxVoQ80H2u6qjAfQ4rv4="
```
例：
```python
class SCookieHandler(RequestHandler):
    def get(self, *args, **kwargs):
        self.set_secure_cookie("wery", "good")
        self.write("ok")
```
存储样子：
```
2|1:0|10:1548248269|5:very|8:Z29vZA==|c611b726829b3ba268e7e01da446a9daed7262b505e29ec34fdf239cef2fcfc8
```
说明：

- 以竖线分割, 冒号前面表示后面有几位
- 安全cookie的版本,默认使用版本2
- 默认为0
- 时间戳
- cookie名
- base64编码的cookie值
- 签名值,不带长度说明

#### 2.获取安全cookie
```python
self.get_secure_cookie(name, value=None, max_age_days=31, min_version=None)
```
说明一: 如果cookie存在且验证通过,返回cookie值,否则返回None

说明二: max_age_days不同于expires_days,expires_days设置浏览器中的cookie的有效时间.而max_age_days是过滤安全cookie的时间戳

例：
```python
class GetSCookieHandler(RequestHandler):
    def get(self, *args, **kwargs):
        scookie = self.get_secure_cookie("very")
        print("scookie =", scookie)
        self.write("ok")
```
注：
安全cookie其实并不安全,只是增加了破解cookie的难度,不要使用cookie存储敏感数据。