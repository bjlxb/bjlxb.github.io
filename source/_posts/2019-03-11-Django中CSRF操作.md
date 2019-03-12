---
layout: photo
title: Django中CSRF操作
tags:
  - Django
date: 2019-03-11 22:17:46
categories: Django
photos:
---
Django通过中间件 django.middleware.csrf.CsrfViewMiddleware 来防止跨站请求伪造，可以通过全局或局部设置来防止跨站请求伪造。
<!--more-->
## 1.CSRF基本使用
```django
<form method="post">
{% csrf_token %}
```
## 2.禁用或启用CSRF
#### 2.1.全局禁用
```python
# 'django.middleware.csrf.CsrfViewMiddleware'
```
#### 2.2.局部禁用
为当前函数强制设置防跨站请求伪造功能，即便settings中禁用了CSRF
```python
from django.shortcuts import render
from django.views.decorators.csrf import csrf_exempt

@csrf_exempt
def my_view(request):
    c = {}
    # ...
    return render(request, "a_template.html", c)
```
#### 2.3.局部启用
为当前函数强制设置防跨站请求伪造功能，即便settings中禁用了CSRF
```python
from django.shortcuts import render
from django.views.decorators.csrf import csrf_protect

@csrf_protect
def my_view(request):
    c = {}
    # ...
    return render(request, "a_template.html", c)
```
## 3.普通FORM表单的POST提交
```django
<form method="post">
{% csrf_token %}
{{ csrf_input }}
</form>
```
## 4.AJAX
#### 4.1.HTML中有FORM表单的AJAX
若HTML中有FORM表单，使用Ajax的POST请求较为简单，只需要获取页面的CSRF token就可以成功提交至后台。
**HTML：**
```html
<form method="post">
{% csrf_token %}
</form>
```
**javascript**
```javascript
<script type="text/javascript">
// using jQuery
var csrftoken = jQuery("[name=csrfmiddlewaretoken]").val();
</script>
```
#### 4.2.HTML中无FORM表单，直接使用AJAX进行POST提交
有时候我们页面并没有FORM表单，却需要使用POST提交数据，因为cookie中存放着CSRF token，故我们可以通过cookie获取。
```javascript
// using jQuery
function getCookie(name) {
    var cookieValue = null;
    if (document.cookie && document.cookie !== '') {
        var cookies = document.cookie.split(';');
        for (var i = 0; i < cookies.length; i++) {
            var cookie = jQuery.trim(cookies[i]);
            // Does this cookie string begin with the name we want?
            if (cookie.substring(0, name.length + 1) === (name + '=')) {
                cookieValue = decodeURIComponent(cookie.substring(name.length + 1));
                break;
            }
        }
    }
    return cookieValue;
}
var csrftoken = getCookie('csrftoken');
</script>
```
通过使用["JavaScript Cookie library"](https://github.com/js-cookie/js-cookie/)库替换以上代码可以简化getCookie：
```javascript
var csrftoken = Cookies.get('csrftoken');
```
当POST请求需要CSRF token，而GET请求不需要提交CSRF token，可以添加如下代码：
```javascript
function csrfSafeMethod(method) {
    // these HTTP methods do not require CSRF protection
    return (/^(GET|HEAD|OPTIONS|TRACE)$/.test(method));
}
$.ajaxSetup({
    beforeSend: function(xhr, settings) {
        if (!csrfSafeMethod(settings.type) && !this.crossDomain) {
            xhr.setRequestHeader("X-CSRFToken", csrftoken);
        }
    }
});
```
###### 参考链接：https://docs.djangoproject.com/en/2.2/ref/csrf/ 