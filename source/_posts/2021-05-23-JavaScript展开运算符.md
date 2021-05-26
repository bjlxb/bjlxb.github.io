---
layout: photo
title: JavaScript展开运算符
tags:
  - 前端
date: 2021-05-23 17:51:46
categories: 前端
photos:
---
记录一下展开运算符这个新知识点
<!--more-->
- ES6 里面号新添加了一个运算符 ... ，叫做展开运算符
- 作用是把数组展开
```javascript
let arr = [1, 2, 3, 4, 5];
console.log(...arr);
// 1 2 3 4 5
```
- 合并数组
```javascript
let arr = [1, 2, 3];
let arr2 = [...arr, 6, 7, 8];
console.log(arr2);
//  [1, 2, 3, 6, 7, 8]
```
- 合并对象
```javascript
let obj = {
	name: 'jack',
	age: 18
};
let obj2 = {
	...obj,
	gender:"男"
}
console.log(obj2);
// {name: "jack", age: 18, gender: "男"}
```
- 函数传递参数
```javascript
let arr = [1, 2, 3];
function fn(a, b, c){
	console.log(a);
	console.log(b);
	console.log(c);
}
fn(...arr);
// 1
// 2
// 3
```

