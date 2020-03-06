---
layout: photo
title: Windows配置Allure Test Report环境
tags:
  - 测试
date: 2020-02-17 23:21:45
categories: 测试
photos:
---
相对于目前常用的测试报告框架，Allure Test Report具有更好看，跨平台等优势！这里主要记录一下在Windows平台下配置Allure Test Report环境！
<!--more-->
#### 1. 安装Scoop
1.1 在PowerShell中输入如下内容（将会安装到默认目录C:\Users\user(自己的用户名)\scoop，也可指定安装目录）：

```powershell
iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
```

1.2想要指定安装目录，在PowerShell中输入如下内容（代码中的D:\Applications\Scoop为指定的目录）：
```powershell
[environment]::setEnvironmentVariable('SCOOP','D:\Applications\Scoop','User')
$env:SCOOP='D:\Applications\Scoop'
iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
```
#### 2. python生成报告

2.1 生成xml：
```powershell
py.test --alluredir ./result
```
2.2 生产网页：
```powershell
allure generate ./result/ -o ./report/ --clean
```
2.3 打开网页：
```powershell
allure open -h 127.0.0.1 -p 8083 ./report/
```


