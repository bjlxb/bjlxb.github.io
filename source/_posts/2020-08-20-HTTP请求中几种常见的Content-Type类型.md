---
layout: photo
title: HTTP请求中几种常见的Content-Type类型
tags:
  - 测试
date: 2020-08-20 21:12:42
categories: 测试
photos:
---
记录一下请求头中Content-Type常见的取值
<!--more-->
POST请求的数据主体放在body中，服务端根据请求头中的Content-Type字段来获取body的编码方式，进而对数据进行解析。

####  application/x-www-form-urlencoded
最常见的 POST 提交数据的方式，原生Form表单，如果不设置 enctype 属性，默认为application/x-www-form-urlencoded 。

Content-Type被指定为 application/x-www-form-urlencoded，表单数据会转换为键值对并按照 key1=val1&key2=val2 的方式进行编码，key 和 val 会进行 URL 转码。大部分服务端语言都对这种方式有很好的支持。若使用AJAX 提交数据，也可使用这种方式。例如 jQuery，Content-Type 默认值都是”application/x-www-form-urlencoded;charset=utf-8”。

#### multipart/form-data
另一个常见的 POST 数据提交的方式， Form 表单的 enctype 设置为multipart/form-data，它会将表单的数据处理为一条消息，以标签为单元，用分隔符（这就是boundary的作用）分开，类似我们上面Content-Type中的例子。　由于这种方式将数据有很多部分，它既可以上传键值对，也可以上传文件，甚至多个文件。当上传的字段是文件时，会有Content-Type来说明文件类型；Content-disposition，用来说明字段的一些信息。每部分都是以 –boundary 开始，紧接着是内容描述信息，然后是回车，最后是字段具体内容（字段、文本或二进制等）。如果传输的是文件，还要包含文件名和文件类型信息。消息主体最后以 –boundary– 标示结束。

#### application/json
Content-Type: application/json 作为响应头比较常见。实际上，现在越来越多的人把它作为请求头，用来告诉服务端消息主体是序列化后的 JSON 字符串，其中一个好处就是JSON 格式支持比键值对复杂得多的结构化数据。由于 JSON 规范的流行，除了低版本 IE 之外的各大浏览器都原生支持JSON.stringify，服务端语言也都有处理 JSON 的函数，使用起来没有困难。Google 的 AngularJS 中的 Ajax 功能，默认就是提交 JSON 字符串。
