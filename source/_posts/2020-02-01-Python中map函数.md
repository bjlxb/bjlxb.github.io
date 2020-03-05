---
layout: photo
title: Python中map函数
tags:
  - Python
date: 2020-02-01 18:37:16
categories: Python
photos:
---

阅读Python进阶书籍时，看到map函数，觉得很有用，记录一下该函数的详细用法！

<!--more-->
map()是Python内置函数。
map()函数的格式是：
```python
map(function, iterable, ...)
```
map()函数接收两个参数：
	1. function 是对iterable进行操作的功能函数
	2. iterable 是一个或多个可迭代对象，用逗号隔开
若function为None，作用同zip()。
map()函数返回值：
	Python2： 直接返回一个新列表，原iterable不变
	Python3： 得到新的map对象，可用list(map_obj)或tuple(map_obj)转化为想要的数据类型

#### 1. 当iterable只有一个
例1：

```python
items = [1, 2, 3, 4, 5]
squared = []
for i in items:
	squared.append(i**2)
# squared = [1, 4, 9, 16, 25]
# 用map实现：
items = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x**2, items))
# squared = [1, 4, 9, 16, 25]
```

例2：

```python
def multiply(x):
	return (x*x)
def add(x):
	return (x+x)

funcs = [multiply, add]
for i in range(5):
	value = map(lambda x: x(i), funcs)
	print(list(value))

# 注:上面print时,加了list转换,是为了python2/3的兼容性
# 在python2中map直接返回列表,但在python3中返回迭代器
# 因此为了兼容python3, 需要list转换一下
# Output:# [0, 0]
# [1, 2]
# [4, 4]
# [9, 6]
# [16, 8]
```
#### 2. 当iterable多于一个

例3：

```python
result = map(lambda x, y: x + y, [1, 3, 5, 7, 9], [2, 4, 6, 8, 10])
# result = [3, 7, 11, 15, 19]
```

注：

​	当function函数时None时，这就同zip()函数了，并且zip()开始取代这个了，目的是将多个列表相同位置的元素归并到一个元组。

```python
result = map(None, [2,4,6],[3,2,1])
result = [(2, 3), (4, 2), (6, 1)]
```

#### 3. 使用map()函数可以实现将其他类型的数转换成list

```python
***将元组转换成list***
>>> map(int, (1,2,3))
[1, 2, 3]
***将字符串转换成list***
>>> map(int, '1234')
[1, 2, 3, 4]
***提取字典的key，并将结果存放在一个list中***
>>> map(int, {1:2,2:3,3:4})
[1, 2, 3]
***字符串转换成元组，并将结果以列表的形式返回***
>>> map(tuple, 'agdf')
[('a',), ('g',), ('d',), ('f',)]
# 将小写转成大写
def u_to_l (s):
  return s.upper()
print map(u_to_l,'abcdef')
['A', 'B', 'C', 'D', 'E', 'F']
```

