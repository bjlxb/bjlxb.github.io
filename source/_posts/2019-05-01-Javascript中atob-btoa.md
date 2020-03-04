---
layout: photo
title: Javascript中atob/btoa
tags:
  - 前端
date: 2019-05-01 22:59:36
categories: 前端
photos:
---
由于网络通讯协议的限制,必须对原数据进行编码后，才能进行发送。 
<!--more-->
WindowOrWorkerGlobalScope.btoa()  从 String 对象中创建一个 base-64 编码的 ASCII 字符串，其中字符串中的每个字符都被视为一个二进制数据字节。

#### 语法
```javascript
let encodedData = window.btoa(stringToEncode);
```
###### 参数
stringToEncode
	一个字符串, 其字符分别表示要编码为 ASCII 的二进制数据的单个字节。
###### 返回值
	一个包含 stringToEncode 的 Base64 表示的字符串。
###### 示例
```javascript
let encodedData = window.btoa("Hello, world"); // base64 编码
let decodedData = window.atob(encodedData); // 解码 成 ASCII
```
#### Unicode 字符串
在多数浏览器中，使用btoa() 对Unicode字符串进行编码都会触发InvalidCharacterError异常。

一种选择是转义任何扩展字符，以便实际编码的字符串是原始字符的ASCII表示形式。考虑这个例子，代码来自Johan Sundström：
```javascript
// ucs-2 string to base64 encoded ascii
function utoa(str) {
    return window.btoa(unescape(encodeURIComponent(str)));
}
// base64 encoded ascii to ucs-2 string
function atou(str) {
    return decodeURIComponent(escape(window.atob(str)));
}
// Usage:
utoa('✓ à la mode'); // 4pyTIMOgIGxhIG1vZGU=
atou('4pyTIMOgIGxhIG1vZGU='); // "✓ à la mode"

utoa('I \u2661 Unicode!'); // SSDimaEgVW5pY29kZSE=
atou('SSDimaEgVW5pY29kZSE='); // "I ♡ Unicode!"
```
更好，更可靠，更廉价的解决方案是使用类型化数组进行转换。

[参考链接](https://developer.mozilla.org/zh-CN/docs/Web/API/WindowBase64/btoa)