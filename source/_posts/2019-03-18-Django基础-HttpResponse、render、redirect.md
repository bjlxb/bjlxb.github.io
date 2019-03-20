---
layout: photo
title: Django常用响应(HttpResponse、render、redirect)
tags:
  - Django
date: 2019-03-18 22:39:00
categories: Django
photos:
---
列举Django常用的响应。
<!--more-->
## HttpResponse
将字符串参数返回给浏览器
```django
from django.shortcuts import HttpResponse

def index(request):
	# 业务逻辑
    return HttpResponse("OK")
```
## JsonResponse
JsonResponse是HttpResponse的子类。
JsonResponse是将数据转换为json字符串后再返回给客户端
JsonResponse自动设置响应头Content-Type为application/json
```django
from django.http import JsonResponse

def index(request):
	# 业务逻辑
    return JsonResponse({"key":value})
```
JsonResponse接受非字典类型的数据，需要指定safe=False
```django
from django.http import JsonResponse

def index(request):
	# 业务逻辑
    return JsonResponse(数字、字符串、列表等,safe=False)
```
## render
from django.shortcuts import render

render三个参数，第一个参数request，第二个参数需要渲染的模板，第三个参数需要返回的数据，以字典的形式。
```django
def index(request):
	# 业务逻辑代码
	return render(request, "index.html", {})
```
## render_to_response
render_to_response与render相似，但只需要两个参数，第一个参数需要渲染的模板，第二个参数需要返回的数据，以字典的形式。
```django
from django.shortcuts import render_to_response

def index(request):
	# 业务逻辑代码
	return render(request, "index.html", {})
​```from django.shortcuts import render_to_response
## redirect
参数为URL，表示让浏览器重定向到指定网址。
​```django
from django.shortcuts import redirect

def index(request):
	# 业务逻辑代码
	return redirect("URL")
```
## 重定向
可以重定向到其他方法中
```django
from django.http import HttpResponseRedirect

def index(request):
	# 业务逻辑代码
	return HttpResponseRedirect("redirecturl")

from django.core.urlresolvers import reverse  
from django.shortcuts import redirect  

def index(request):
	# 业务逻辑代码
	return redirect(reverse('方法', args=参数))
```