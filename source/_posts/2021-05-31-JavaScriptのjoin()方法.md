---
layout: photo
title: JavaScriptのjoin()方法
tags:
  - 前端
date: 2021-05-31 20:41:16
categories: 前端
photos:
---
记录一下JavaScript中join()的使用！
<!--more-->
### 定义和用法

join() 方法将数组中的所有元素拼接为一个字符串。
元素可以通过指定的分隔符进行分隔的。

### 语法

```javascript
arrayObject.join(separator)
// separator：可选,指定要使用的分隔符。省略该参数，默认使用逗号作为分隔符。
```
### 返回值

返回一个字符串，通过把arrayObject中的每个元素转换为字符串，然后把这些字符串连接起来，每个元素之间插入separator分隔符。

### 实例

##### 例1:
```javascript
var arr = new Array(3)
arr[0] = "张三"
arr[1] = "李四"
arr[2] = "王五"
console.log(arr.join())

// 张三,李四,王五
```

##### 例2:
```javascript
var arr = new Array(3)
arr[0] = "山东省"
arr[1] = "烟台市"
arr[2] = "莱山区"
console.log(arr.join("."))

// 山东省.烟台市.莱山区
```