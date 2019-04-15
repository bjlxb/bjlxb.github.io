---
layout: photo
title: Mac下安装配置Mongodb
tags:
  - null
date: 2019-04-13 23:36:06
categories:
photos:
---
MongoDB作为著名的Nosql数据库,在许多方面都有很大的作用,可以快速搭建一个登录注册系统.
<!--more-->
## 一.使用homebrew安装
#### 1.进入https://brew.sh,使用命令安装homebrew
```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
# 卸载命令
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"
```
#### 2.安装mongodb
```bash
brew install mongodb
```
#### 3.启动mongodb
```bash
brew services start mongodb
```
#### 4.进入mongodb的shell
```bash
mongo
```
#### 查看mongodb进程
```bash
ps -aef | grep mongo
```
## 二.mongodb常用命令：
#### 查询库
```
//查询所有的数据库
show dbs  
```
#### 查询表
```
//查询当前数据库下的所有数据表
show collections   
```
#### 建库和删库
```
//建立一个名为myDbs的数据库，当这个库存在时则是切换到这个数据库中去
use myDbs  

//这两句是删除这个数据库
use myDbs
db.dropDatabase();  
```
#### 建表和删表
```
//表操作都是要先到一个数据库中去，通过use方法
//在mongodb中在插入数据时即创建了表，此时创建的是名为myTable的数据表
db.myTable.insert({name:’hf’,age:20});  
//删除myTable这个数据表
db.myTable.drop();  
//如果没有指定数据库，表会创建在mongdb默认数据库test里
```
#### 单表的增删改
```
//新增
db.myTable.insert({name:’hahaha’,age:12});  
//修改
db.myTable.update({name:’hf’},{$set:{age:25}})  
//删除
db.myTable.remove({name:’hf'});  
```
#### 查询
```
//查询myTable中的所有数据
db.myTable.find();  
//根据age升续
db.myTable.find().sort({age:1})  
//查询
db.myTable.find().count();  
```

