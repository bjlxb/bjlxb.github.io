---
layout: photo
title: 设置input中placeholder的字体样式
tags:
  - 前端
date: 2019-04-20 21:10:33
categories: 前端
photos:
---
项目中遇到需要修改input的placeholder样式
<!--more-->
#### 注：
placeholder属性是css3中新增加的属性，IE9和Opera12以下版本的CSS选择器均不支持占位文本。
#### 设置placeholder样式
###### 方式1
每个浏览器的CSS选择器都有所差异，所以针对每个浏览器都需要单独的设定(可以在冒号前面写input和textarea)。
```css
::-webkit-input-placeholder { /* WebKit browsers */
　　color:#999;font-size:16px;
}
:-moz-placeholder { /* Mozilla Firefox 4 to 18 */
　　color:#999;font-size:16px;
}

::-moz-placeholder { /* Mozilla Firefox 19+ */
　　color:#999;font-size:16px;
}

:-ms-input-placeholder { /* Internet Explorer 10+ */
　　color:#999;font-size:16px;
}
```
###### 方式2（推荐）
在手机客户端webview 只使用－webkit内核方式即可。
```css
input::-webkit-input-placeholder, textarea::-webkit-input-placeholder {
　　color: #666;font-size:16px;
}

input:-moz-placeholder, textarea:-moz-placeholder {
　　color:#666;font-size:16px;
}

input::-moz-placeholder, textarea::-moz-placeholder {
　　color:#666;font-size:16px;
}

input:-ms-input-placeholder, textarea:-ms-input-placeholder {
　　color:#666;font-size:16px;
}
```

[参考链接](https://www.cnblogs.com/overstackcoder/p/5522637.html)

