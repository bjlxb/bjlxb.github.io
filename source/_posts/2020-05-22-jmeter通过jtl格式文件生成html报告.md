---
layout: photo
title: jmeter通过jtl格式文件生成html报告
tags:
  - 测试
date: 2020-05-22 22:32:07
categories: 测试
photos:
---
有时在使用jmeter时，会出现未生成html报告的情况，需要通过jtl文件生成html报告。
<!--more-->
通过命令生成html格式报告
```
jmeter -g jtl文件 -o 生成html文件夹
# 注：html文件夹必须是存在的，不然会报错！
```

