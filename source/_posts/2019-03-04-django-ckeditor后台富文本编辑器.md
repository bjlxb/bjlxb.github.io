---
layout: photo
title: django-ckeditor后台富文本编辑器
date: 2019-03-04 22:36:17
tags:
  - Django
categories: Django
photos:
---
Django很多富文本已经很久没有维护了，django-ckeditor使用方便，配置简单，还支持图片上传。具体说明可见[pypi](https://pypi.org/project/django-ckeditor/)
<!--more-->
## 一、简单使用django-ckeditor ##
##### 1）安装django-ckeditor #####
使用pip安装，现在最新版本是5.6.1：

	pip install django-ckeditor
##### 2）注册应用 #####
在django项目中，找到settings.py文件中的INSTALLED_APPS加入'ckeditor'：

	INSTALLED_APPS = [
    'ckeditor',
	]

##### 3）修改模型 #####

在模型文件models.py中修改字段为富文本编辑：
	
	from django.db import models


	class Activity(models.Model):
    	activity_name = models.CharField(max_length=20, verbose_name="活动名称")
    	activity_simple_depict = models.CharField(max_length=50, verbose_name="简单描述")
    	activity_depict = models.TextField(verbose_name="活动描述")

将活动描述更改为富文本：

	from django.db import models
	from ckeditor.fields import RichTextField

	class Activity(models.Model):
    	activity_name = models.CharField(max_length=20, verbose_name="活动名称")
    	activity_simple_depict = models.CharField(max_length=50, verbose_name="简单描述")
    	activity_depict = RichTextField('活动描述')

![](https://i.imgur.com/I7miQIC.jpg)

需要简体中文，设置settings.py的LANGUAGE_CODE = 'zh-hans'。

注：zh-hans都是小写。

若写为zh-Hans，会显示为繁体。

另外，此时无法从本地上传图片，只能使用网络图片。可添加上传图片功能。



