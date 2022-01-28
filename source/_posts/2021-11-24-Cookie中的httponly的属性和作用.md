---
layout: photo
title: Cookie中的httponly的属性和作用
tags:
  - 前端
date: 2021-11-24 21:47:02
categories: 前端
photos:
---
偶尔接触到Cookie中的httponly的属性，学习下。
<!--more-->
#### HttpOnly是什么
cookie中设置了HttpOnly属性，通过js脚本无法读取到cookie信息，能有效的防止XSS攻击，窃取cookie内容，增加cookie的安全性，但是也不要将重要信息存入cookie中。
XSS全称Cross SiteScript，跨站脚本攻击，是Web程序中常见的漏洞，XSS属于被动式且用于客户端的攻击方式，所以容易被忽略其危害性。
XSS的原理是攻击者向有XSS漏洞的网站中输入(传入)恶意的HTML代码，当其它用户浏览该网站时，这段HTML代码会自动执行，达到攻击的目的。如：盗取用户Cookie、破坏页面结构、重定向到其它网站等。

#### HttpOnly的设置样例

```javascript
response.setHeader( "Set-Cookie" , "cookiename=httponlyTest;Path=/;Domain=domainvalue;Max-Age=seconds;HTTPOnly");
// 例如：
// 设置cookie
response.addHeader("Set-Cookie", "uid=112; Path=/; HttpOnly")

// 设置多个cookie
response.addHeader("Set-Cookie", "uid=112; Path=/; HttpOnly");
response.addHeader("Set-Cookie", "timeout=30; Path=/test; HttpOnly");

// 设置https的cookie
response.addHeader("Set-Cookie", "uid=112; Path=/; Secure; HttpOnly");
```
设置完毕后通过js脚本是读不到该cookie的，但使用如下方式可以读取。
```javascript
Cookie cookies[]=request.getCookies(); 
```
