---
layout: photo
title: Django中的request对象
tags:
  - Django
date: 2019-03-29 22:38:12
categories: Django
photos:
---
Django中经常使用request对象的方法,做一下总结!
<!--more-->
HttpRequest对象的属性

| 属性                  | 描述                                                         |
| ------------------ | --------------------------- |
| path                  | 表示提交请求页面完整地址的字符串，不包括域名，如 "/music/bands/the_beatles/"。 |
| path_info | 获取具有 URL 扩展名的资源的附加路径信息。相对于HttpRequest.path，使用该方法便于移植。 |
| scheme | 请求的协议，一般为http或者https，字符串格式(以下属性中若无特殊指明，均为字符串格式) |
| body | http请求的主体，二进制格式。 |
| method                | 表示提交请求使用的HTTP方法。它总是大写的。例如：if request.method == 'GET':    do_something()elif request.method == 'POST':    do_something_else() |
| GET                   | 一个类字典对象，包含所有的HTTP的GET参数的信息。见 QueryDict 文档。 |
| POST                  | 一个类字典对象，包含所有的HTTP的POST参数的信息。见 QueryDict 文档。通过POST提交的请求有可能包含一个空的 POST 字典，也就是说， 一个通过POST方法提交的表单可能不包含数据。因此，不应该使用 if request.POST 来判断POST方法的使用，而是使用 if request.method == "POST" （见表中的 method 条目）。注意： POST 并 不 包含文件上传信息。见 FILES 。 |
| REQUEST               | 为了方便而创建，这是一个类字典对象，先搜索 POST ，再搜索 GET 。 灵感来自于PHP的 $_REQEUST 。例如， 若 GET = {"name": "john"} ， POST = {"age": '34'} ，REQUEST["name"] 会是 "john" ， REQUEST["age"] 会是 "34" 。强烈建议使用 GET 和 POST ，而不是 REQUEST 。这是为了向前兼容和更清楚的表示。 |
| COOKIES               | 一个标准的Python字典，包含所有cookie。键和值都是字符串。cookie使用的更多信息见第12章。 |
| FILES                 | 一个类字典对象，包含所有上传的文件。 FILES 的键来自 <input type="file" name="" /> 中的 name 。 FILES 的值是一个标准的Python字典，包含以下三个键：filename ：字符串，表示上传文件的文件名。content-type ：上传文件的内容类型。content ：上传文件的原始内容。注意 FILES 只在请求的方法是 POST ，并且提交的 <form> 包含enctype="multipart/form-data" 时才包含数据。否则， FILES 只是一个空的类字典对象。 |
| META                  | 一个标准的Python字典，包含所有有效的HTTP头信息。有效的头信息与客户端和服务器有关。这里有几个例子：CONTENT_LENGTHCONTENT_TYPEQUERY_STRING ：未解析的原始请求字符串。REMOTE_ADDR ：客户端IP地址。REMOTE_HOST ：客户端主机名。SERVER_NAME ：服务器主机名。SERVER_PORT ：服务器端口号。在 META 中有效的任一HTTP头信息都是带有 HTTP_ 前缀的键，例如：HTTP_ACCEPT_ENCODINGHTTP_ACCEPT_LANGUAGEHTTP_HOST ：客户端发送的 Host 头信息。HTTP_REFERER ：被指向的页面，如果存在的。HTTP_USER_AGENT ：客户端的user-agent字符串。HTTP_X_BENDER ： X-Bender 头信息的值，如果已设的话。 |
| user                  | 一个 django.contrib.auth.models.User 对象表示当前登录用户。 若当前用户尚未登录， user 会设为 django.contrib.auth.models.AnonymousUser 的一个实例。可以将它们与 is_authenticated() 区别开：if request.user.is_authenticated():    # Do something for logged-in users.else:    # Do something for anonymous users.user 仅当Django激活 AuthenticationMiddleware 时有效。关于认证和用户的完整细节，见第12章。 |
| site | 中间件属性 |
| session               | 一个可读写的类字典对象，表示当前session。仅当Django已激活session支持时有效。见第12章。 |
| raw_post_data         | POST的原始数据。 用于对数据的复杂处理。                      |
| encoding | 获取请求中表单提交数据的编码。 |
| content_type | 获取请求的MIME类型(从CONTENT_TYPE头部中获取)，django1.10的新特性。 |
| content_params | 取CONTENT_TYPE中的键值对参数，并以字典的方式表示，django1.10的新特性。 |
|  |  |

-----------

HttpRequest 的方法

| 方法                 | 描述                                                         |
| ------------------ | --------------------------- |
| get_host()                   | 返回请求的源主机。example: 127.0.0.1:8000                    |
| get_port()                   | django1.9的新特性。                                          |
| bulid_absolute_uri(location) | 返回location的绝对uri，location默认为request.get_full_path()。 |
|                              |                                                              |
| __getitem__(key)             | 请求所给键的GET/POST值，先查找POST，然后是GET。若键不存在，则引发异常KeyError 。该方法使用户可以以访问字典的方式来访问一个 HttpRequest 实例。例如， request["foo"] 和先检查 request.POST["foo"] 再检查request.GET["foo"] 一样。 |
| has_key()                    | 返回 True 或 False ，标识 request.GET 或 request.POST 是否包含所给的键。 |
| get_full_path()              | 返回 path ，若请求字符串有效，则附加于其后。例如，"/music/bands/the_beatles/?print=true" 。 |
| is_secure()                  | 如果请求是安全的，则返回 True 。也就是说，请求是以HTTPS的形式提交的。 |

[参考链接1](https://docs.djangoproject.com/zh-hans/2.1/_modules/django/http/request/)

[参考链接2](https://www.cnblogs.com/eric_yi/p/8046586.html)

