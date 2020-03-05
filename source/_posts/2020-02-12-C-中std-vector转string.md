---
layout: photo
title: 'C++中std::vector转string'
tags:
  - C/C++
date: 2020-02-12 21:32:27
categories: C/C++
photos:
---
在C++中将std::vector<string>在不经过for遍历的前提下转为string
<!--more-->
#### 1. accumulate函数
```c++
#include <vector>
#include <string>
#include <numeric> //accumulate需要
#include <iostream>
int main()
{
    std::string str;
    std::vector<std::string> list;
    list.push_back("hello");
    list.push_back("world");
    str = accumulate(list.begin(), list.end(), str);
    std::cout<<str.c_str()<<std::endl;
}

// 输出
helloworld
```

