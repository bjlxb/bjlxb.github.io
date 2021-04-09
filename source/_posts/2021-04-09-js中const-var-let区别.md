---
layout: photo
title: 'js中const,var,let区别'
tags:
  - 前端
date: 2021-04-09 10:32:58
categories: 前端
photos:
---
js中三种定义变量的方式const， var， let的区别。
<!--more-->
1. const定义的变量不可以修改，而且必须初始化
```javascript
const a = 1;//正确
// const a;//错误，必须初始化 
console.log('函数外const定义a：' + a);//有输出值
// a = 2;
// console.log('函数外修改const定义a：' + a);//无法输出 
```
2. var定义的变量可以修改，如果不初始化会输出undefined，不会报错
```javascript
var a = 1;
// var a;//不会报错
console.log('函数外var定义a：' + a);//可以输出a=1
function change(){
	a = 2;
	console.log('函数内var定义a：' + a);//可以输出a=2
} 
change();
console.log('函数调用后var定义a为函数内部修改值：' + a);//可以输出a=2
```
3. let是块级作用域，函数内部使用let定义后，对函数外部无影响
```javascript
let a = 1;
console.log('函数外let定义a：' + a);//输出c=1
function change(){
	let a = 2;
	console.log('函数内let定义a：' + a);//输出c=2
} 
change();
console.log('函数调用后let定义a不受函数内部定义影响：' + a);//输出a=1
```

