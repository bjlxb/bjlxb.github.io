---
layout: photo
title: 在阿里云服务器上部署nginx+uWSGI+Django
tags:
  - Django
date: 2019-03-06 19:38:20
categories: Django
photos:
---
公司小程序上线，需要在阿里云Centos服务器上部署，使用nginx+uWSGI+Django来部署服务器。
<!--more-->
## 第一步：前期准备工作 ##
1.因为测试期间使用的sqlite3数据库，考虑是否更换为mysql和oracle数据库，提前将settings中配置好，是很有必要的。
2.将测试环境使用的工具包收集，收集命令为：
{% codeblock lang:python %}
	pip freeze > requirements.txt
{% endcodeblock %}
安装命令为：
{% codeblock lang:python %}
	pip install -r requirements.txt
{% endcodeblock %}
3.修改ALLOWED_HOSTS，同时将DEBUG = True设置为DEBUG = False

4.上传目录到服务器

	scp  -r local_dir username@servername:remote_dir

## 第二步：配置uWSGI ##
##### 1.安装uWSGI #####
推荐使用pip install uwsgi或pip3 install uwsgi

##### 2.配置uWSGI #####
1.新建uwsgi.ini文件

注：uwsgi.ini文件在django根目录下与manage.py在同一目录下

2.uwsgi.ini内容：
	[uwsgi]

	chdir = /root/project/adv/ppmoney
	module = ppmoney.wsgi:application
	socket = 127.0.0.1:8001 #端口号与nginx内一致
	master = true         
	pidfile = /root/project/adv/ppmoney/uwsgi.pid
	vacuum=True
	max-requests=5000
	daemonize = /root/project/adv/ppmoney/uwsgi_bug.log
	disable-logging = true

详细说明：

	配置项中以‘#’开头的都是被注释的项目，不起作用；
	以双斜杠开头，表示注释；
	chdir是你的项目根目录。我这里的项目名叫for_test；
	moudule是你的入口wsgi模块，将for_test替换成你的项目名称；
	socket是通信端口设置，和我一样就行；
	master=True表示以主进程模式运行；
	demonize是你的日志文件，会自动建立
	disable-logging = true 表示不记录正常信息，只记录错误信息。否则你的日志可能很快就爆满了。
##### 3.启动uWSGI #####
在该目录下使用sudo uwsgi uwsgi.ini启动uwsgi
	uwsgi --ini uwsgi.ini # 启动
	uwsgi --reload uwsgi.pid # 重启
	uwsgi --stop uwsgi.pid # 关闭

## 第三步：配置nginx ##
##### 1.安装nginx #####
Centos使用：
	yum install nginx
Ubuntu使用：
	sudo apt-get update
	sudo apt-get install nginx

##### 2.配置nginx #####
在/etc/nginx/conf.d目录下新建[项目名].conf文件

文件内容：

	server {
	  listen 80;  #启动的nginx进程监听请求的端口
	  server_name ;   #域名或ip
	  location / {
	    include /etc/nginx/uwsgi_params;
	    uwsgi_pass 127.0.0.1:8001;  #对于动态请求，转发到本机的8001端口，也就是uwsgi监听的端口
	  }
	
	  location /static/ {
	    alias /www/data/static/;    #设定静态文件所在目录
	  }
	}
##### 3.启动nginx #####
centos 7之前的系统和Ubuntu使用命令：

	nginx：service nginx start #启动
	nginx：service nginx stop #停止
	nginx：service nginx restart #重启

centos7+系统使用命令：

	systemctl start nginx #启动
	systemctl stop nginx #停止
	systemctl restart nginx #重启

# 问题 #
### 一 django 项目部署后通过 admin 上传的图片的路径问题 ###
有时项目部署后会出现通过 admin 上传图片后，图片会存放在 django 项目的 static/media 目录下，nginx的静态文件目录下没有
###### 解决方案 ######
	MEDIA_ROOT 直接改成 nginx 配置的目录
### 二 通过nginx+uwsgi服务器部署Django出现的502错误 ###
当同一云服务器配置了多个Django项目时，会出现该问题,
查看uWSGI的log会发现错误信息：

	-- unavailable modifier requested: 0 --
###### 解决方案 ######
	1 apt-get install uwsgi-plugin-python #安装 uwsgi-plugin-python
	2 在项目目录uWSGI.ini文件最后一行加入plugins = python
	3. 重启uwsgi-Django项目
	4. 重启nginx
