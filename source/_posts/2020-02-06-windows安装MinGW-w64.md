---
layout: photo
title: windows安装MinGW-w64
tags:
  - C/C++
date: 2020-02-06 22:58:43
categories: C/C++
photos:
---

记录一下Windows安装MinGW-w64的详细过程！

<!--more-->

#### 1. 下载MinGW-w64

  进入[MinGW-w64官网](https://sourceforge.net/projects/mingw-w64/files/mingw-w64/)，选择[x86_64-posix-seh]([x86_64-posix-sjlj](https://sourceforge.net/projects/mingw-w64/files/Toolchains targetting Win64/Personal Builds/mingw-builds/8.1.0/threads-posix/sjlj/x86_64-8.1.0-release-posix-sjlj-rt_v6-rev0.7z))进行下载

#### 2. 解压至指定位置

  使用7-Zip将下载文件解压至指定位置，最好将文件夹名字修改为MinGW-w64，方便后续环境变量配置。

#### 3. 配置环境变量

  1. 此电脑-->右键-->属性
    <img src="/image/MinGW-w64/MinGW-w64-1.png">
  2. 选择高级系统设置
    <img src="/image/MinGW-w64/MinGW-w64-2.png">
  3. 选择环境变量
    <img src="/image/MinGW-w64/MinGW-w64-3.png">
  4. 系统变量-->选中Path-->点击编辑
    <img src="/image/MinGW-w64/MinGW-w64-4.png">
  5. 将MinGW-w64中bin目录地址拷贝
    <img src="/image/MinGW-w64/MinGW-w64-5.png">
  6. 选择新建-->将前面拷贝的地址粘贴
    <img src="/image/MinGW-w64/MinGW-w64-6.png">

#### 4. 验证配置

  1.使用win+r输入cmd或者powershell。
  2.输入gcc -v，回车，出现如下信息说明配置正确。
  <img src="/image/MinGW-w64/MinGW-w64-7.png">

  3. 若不是该信息需检查上面步骤是否都正确！

#### 5. 运行程序

  可以通过g++ xxx.cpp -o xxx.exe命令指令编译c/cpp文件

