---
layout: photo
title: JavaScript截取数组
tags:
  - 前端
date: 2021-04-22 17:52:06
categories: 前端
photos:
---
记录一下JavaScript中截取数组函数slice
<!--more-->
### slice定义和用法
slice() 可从已有的数组中返回选定的元素。
### 语法
arrayObject.slice(start,end)

| 参数  | 描述                                                         |
| :---- | :----------------------------------------------------------- |
| start | 必需。规定从何处开始选取。如果是负数，那么它规定从数组尾部开始算起的位置。也就是说，-1 指最后一个元素，-2 指倒数第二个元素，以此类推。 |
| end   | 可选。规定从何处结束选取。该参数是数组片断结束处的数组下标。如果没有指定该参数，那么切分的数组包含从 start 到数组结束的所有元素。如果这个参数是负数，那么它规定的是从数组尾部开始算起的元素。 |

### 返回值
返回一个新的数组，包含从 start 到 end （不包括该元素）的 arrayObject 中的元素。

### 注意：
该方法不能修改数组，而是返回一个子数组。如果想删除数组中的一段元素，应该使用方法 Array.splice()。

### 说明
使用负值从数组的尾部选取元素。
如果 end 未被规定，那么 slice() 方法会选取从 start 到数组结尾的所有元素。

### 案例1

```javascript
<script type="text/javascript">
 
var arr = new Array(3)
arr[0] = "张三"
arr[1] = "李四"
arr[2] = "王五"
 
console.log(arr)
console.log(arr.slice(1))
console.log(arr)
</script>

// ["张三", "李四", "王五"]
// ["李四", "王五"]
// ["张三", "李四", "王五"]
```

### 案例2

```javascript
<script type="text/javascript">
 
var arr = new Array(6)
arr[0] = "张三"
arr[1] = "李四"
arr[2] = "王五"
arr[3] = "赵六"
arr[4] = "孙七"
arr[5] = "周八"
 
console.log(arr)
console.log(arr.slice(2,4))
console.log(arr)
 
</script>

// ["张三", "李四", "王五", "赵六", "孙七", "周八"]
// ["王五", "赵六"]
// ["张三", "李四", "王五", "赵六", "孙七", "周八"]
```

### 案例3

```javascript
<script type="text/javascript">
//JS Array.slice 截取数组
//在JavaScript中，Array对象的slice(start[,end])方法返回数组从下标[start,end)的部分（不包含下标为end的元素）如果没有指定end参数，则从start开始到数组结尾的部分，slice()方法不改变原数组，如果要删除数组的一部分，可以使用splice()方法。
//参数：
//（1）start:开始截取的数组下标，如果start是负数，表明从数组尾部开始计算。
//（2）end:结束截取的数组下标，如果end是负数，表明从数组尾部开始计算。
 
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];

console.log(arr.slice(5));
console.log(arr.slice(-5));
console.log(arr.slice(0,3));
console.log(arr.slice(1,2));
console.log(arr.slice(3,-2));
console.log(arr.slice(1,9999));

// [6, 7, 8, 9]
// [5, 6, 7, 8, 9]
// [1, 2, 3]
// [2]
// [4, 5, 6, 7]
// [2, 3, 4, 5, 6, 7, 8, 9]

//==================================================================================================

</script>
```

### 案例4

```javascript
<script>
//JS Array.splice(start,delete_count,value,...) 插入、删除、替换数组
//参数：
//（1）start:开始插入和（或）删除的数组元素的下标。
//（2）delete_count:结束截取的数组下标，如果end是负数，表明从数组尾部开始计算。
//（3）value,...：要插入数组的元素。
//返回：如果从数组中删除了元素，则返回的是被删除的元素的数组

var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
console.log("arr=" + arr);
console.log("arr.splice(5)=" + arr.splice(5));
console.log("arr=" + arr);

// arr=1,2,3,4,5,6,7,8,9
// arr.splice(5)=6,7,8,9
// arr=1,2,3,4,5

var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
console.log("arr=" + arr);
console.log("arr.splice(5,1,99,100)=" + arr.splice(5,1,99,100));
console.log("arr=" + arr);

// arr=1,2,3,4,5,6,7,8,9
// arr.splice(5,1,99,100)=6
// arr=1,2,3,4,5,99,100,7,8,9
</script>
```