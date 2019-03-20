---
layout: photo
title: '报错:ImportError: No module named Crypto.Hash'
tags:
  - Django
date: 2019-03-20 22:59:49
categories: Django
photos:
---
今天项目中遇到一个报错，试了很多方法才解决，记录一下。
<!--more-->
## 导包出现错误
```python
from Crypto.Hash import SHA, HMAC
# 错误信息
ImportError: No module named Crypto.Hash
```
## 解决方案：
- 不使用虚拟环境，使用如下命令删除已安装的包
```python
sudo pip uninstall crypto
sudo pip uninstall pycrypto
```
-  使用虚拟环境，使用如下命令删除已安装的包
```python
pip uninstall crypto
pip uninstall pycrypto
```
- 不使用虚拟环境，使用如下命令安装pycrypto包
```python
sudo pip install pycrypto
```
- 使用虚拟环境，使用如下命令安装pycrypto包
```python
pip install pycrypto
```


