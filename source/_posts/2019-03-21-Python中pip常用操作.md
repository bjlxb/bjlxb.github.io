---
layout: photo
title: Python中pip常用操作
tags:
  - Python
date: 2019-03-21 22:47:54
categories: Python
photos:
---
简单记录一下Python最常用的包管理工具pip
<!--more-->
确定pip对应Python版本
```
pip -V(大写V)
```
## 安装pip
Python2 版本大于2.7.9或者Python3版本大于3.4都默认安装了pip
若未安装，可以使用如下方式
1. 使用easy_install安装：进入到easy_install脚本的目录下，然后运行**easy_inatall pip**
2. 使用get-pip.py安装： 下载get-pip.py脚本 **curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py** 然后运行：**python get-pip.py** 这个脚本会同时安装setuptools和wheel工具。
3. 在linux下安装pip： 
	- Fedora系下：**sudo yum install python-pip**
	- ubuntu下：**sudo apt-get install python-pip**
4. 在windows下安装pip： 在Python安装目录的scirpts目录下运行**easy_install pip**进行安装
---

## pip使用

命令行中输入pip，查看帮助说明
#### 1.默认安装
```
pip install 第三方模块名
```
#### 2.指定版本
```
pip install 第三方模块名 [=, >=, <=, >, <] 版本号
```
#### 3.卸载安装
```
pip uninstall 第三方模块名
```
#### 4.已安装库
```
pip list
```
#### 5.安装库导出
```
pip freeze > requirements.txt
```
#### 6.据导出批量安装库
```
pip install -r requirements.txt
```
#### 7.安装wheel文件
```
pip install *.whl
```
## 更换pip源
由于网速， GWF等原因，很多时候安装不成功，这时候需要更远数据源来提高下载速度和成功率。
	pip国内的一些镜像
	阿里云 http://mirrors.aliyun.com/pypi/simple/ 
	中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/ 
	豆瓣(douban) http://pypi.douban.com/simple/ 
	清华大学 https://pypi.tuna.tsinghua.edu.cn/simple/ 
	中国科学技术大学 http://pypi.mirrors.ustc.edu.cn/simple/
###### 临时使用  
```
pip install package_name -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install -i  https://pypi.tuna.tsinghua.edu.cn/simple package_name

pip install -i https://pypi.doubanio.com/simple/ --trusted-host pypi.doubanio.com pillow
```
###### 永久修改：
- linux
修改 ~/.pip/pip.conf (没有就创建一个)
```
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple

[install]  
trusted-host=pypi.tuna.tsinghua.edu.cn
disable-pip-version-check = true  
timeout = 6000
```
- windows
在user目录创建pip目录，如：C:\Users\xx\pip，新建文件pip.ini
```
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple

[install]  
trusted-host=pypi.tuna.tsinghua.edu.cn
disable-pip-version-check = true  
timeout = 6000
```