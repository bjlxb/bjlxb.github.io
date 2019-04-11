---
layout: photo
title: Django中FileField同名文件直接覆盖
tags:
  - Django
date: 2019-04-11 23:03:13
categories: Django
photos:
---
Django中FileField默认情况遇到相同文件名的时候会自动在后面加下划线，有时业务需要直接覆盖先前的文件
<!--more-->
### 解决方案
自定义一个mystorage类,继承FileSystemStorage并重写其get_available_name方法.
```
import os
from django.core.files.storage import FileSystemStorage

class mystorage(FileSystemStorage):
    def get_available_name(self, name, max_length=255):
        if self.exists(name):
            os.remove(os.path.join(settings.MEDIA_ROOT, name))
        return name

        
file = models.FileField(upload_to='file/',storage=mystorage())
# 注:get_available_name中max_length参数必须指定,否则在存储文件时出现会报错问题.
```