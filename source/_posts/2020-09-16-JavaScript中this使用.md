---
layout: photo
title: JavaScript中this使用
tags:
  - 前端
date: 2020-09-16 22:23:49
categories: 前端
photos:
---
学习下JavaScript中this关键词
<!--more-->
this 是 JavaScript 语言的一个关键字。

#### this的问题
虽然obj.foo和foo指向同一个函数，但是执行结果可能不一样。
```javascript
var obj = {
  foo: function () {}
};

var foo = obj.foo;

// 写法一
obj.foo()

// 写法二
foo()
```
如下例子，bj.foo和foo虽然指向同一函数，但是执行结果不同。
```javascript
var obj = {
  foo: function () { console.log(this.bar) },
  bar: 1
};

var foo = obj.foo;
var bar = 2;

obj.foo() // 1
foo() // 2
```
  这种差异的原因，就在于函数体内部使用了this关键字。很多教科书会告诉你，this指的是函数运行时所在的环境。对于obj.foo()来说，foo运行在obj环境，所以this指向obj；对于foo()来说，foo运行在全局环境，所以this指向全局环境。所以，两者的运行结果不一样。

------

#### 内存数据结构
JavaScript 语言之所以有this的设计，跟内存里面的数据结构有关系。
```javascript
var obj = { foo:  5 };
```

上面的代码将一个对象赋值给变量obj。JavaScript 引擎会先在内存里面，生成一个对象{ foo: 5 }，然后把这个对象的内存地址赋值给变量obj。

[ 阮一峰博客JavaScript 的 this 原理](http://www.ruanyifeng.com/blog/2018/06/javascript-this.html)

