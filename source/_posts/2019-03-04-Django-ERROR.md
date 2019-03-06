---
layout: photo
title: Django-ERROR
date: 2019-03-04 19:17:59
tags:
  - Django
categories: Django
photos:
  - https://cn.bing.com/az/hprichbg/rb/FinWhale_ZH-CN9010064973_1920x1080.jpg
  - https://cn.bing.com/az/hprichbg/rb/HZMB_ZH-CN5238831909_1920x1080.jpg
---
<!--more-->
# Django中的Error #
出现<font color="#FF0000">UNICODEENCODEERROR: 'ASCII' CODEC CAN'T ENCODE CHARACTERS IN POSITION 2-5: ORDINAL NOT IN RANGE(128)</font>错误
<!--more-->
解决方案：
字符集出现问题，在文件前加两行代码解决问题。
{% codeblock lang:python %}
	reload(sys)
	sys.setdefaultencoding('utf-8')
{% endcodeblock %}
    