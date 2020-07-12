---
layout: photo
title: C++中int与string的相互转换
tags:
  - C/C++
date: 2020-02-23 23:50:27
categories: C/C++
photos:
---
在C++中经常会遇到类型转换问题，这里主要记录一下C++中int和string类型的相互转换！
<!--more-->
一、int转换成string
1.1 to_string函数
```c++
// c++11标准增加了全局函数std::to_string:

string to_string (int val);
string to_string (long val);
string to_string (long long val);
string to_string (unsigned val);
string to_string (unsigned long val);
string to_string (unsigned long long val);
string to_string (float val);
string to_string (double val);
string to_string (long double val);
// to_string例子
#include <iostream>   // std::cout  
#include <string>     // std::string, std::to_string  
  
int main ()  
{  
  std::string pi = "圆周率：" + std::to_string(3.14);  
  std::string perfect = std::to_string(6+6+6+6+6) + "是一个很好的数字！";  
    
  std::cout << pi << '\n';  
  std::cout << perfect << '\n';  
  return 0;  
} 
// 输出
// 圆周率：3.14
// 30是一个很好的数字！

```

1.2 字符串流

- 标准库定义了三种类型字符串流：istringstream,ostringstream,stringstream，分别可以读、写以及读和写string类型,它们是由iostream类型派生而来的。

- 要使用它们需要包含sstream头文件。

- sstream类型定义了一个有string形参的构造函数，即：stringstream stream(str); 创建了存储str副本的stringstream对象，str为string类型对象。

- 定义了名为str的成员，用来读取或设置stringstream对象所操纵的string值：stream.str(); 返回stream中存储的string类型对象stream.str(str); 将string类型的s复制给stream，返回void。

```c++
int num = 30;
stringstream s;
s<<num; 
string str = s.str();
cout<<str<<endl; 

// 输出
// 30
```

二、string转换成int

2.1 采用标准库中atoi函数
- 其他类型也都有对应的标准库函数，比如浮点型atof(),long型atol()。
```c++
std::string str = "123";
int n = atoi(str.c_str());
cout<<n; 
// 输出
// 123
```
2.2 使用sstream头文件中定义的字符串流对象

```c++
//构造输入字符串流，流的内容初始化为“12”的字符串
istringstream is("123");
int num;
//从is流中读入一个int整数存入i中
is >> num;
```

