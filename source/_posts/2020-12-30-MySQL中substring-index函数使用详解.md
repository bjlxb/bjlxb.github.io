---
layout: photo
title: MySQL中substring_index函数使用详解
tags:
  - DB
date: 2020-12-30 19:40:49
categories: DB
photos:
---
substring_index函数使用详解
<!--more-->
## 定义

SUBSTRING_INDEX - 按分隔符截取字符串

## 语法

```mysql
SUBSTRING_INDEX(str, delimiter, count);
```

返回一个 str 的子字符串，在 delimiter 出现 count 次的位置截取。
如果 count > 0，从则左边数起，且返回位置前的子串；如果 count < 0，从则右边数起，且返回位置后的子串。
delimiter 是大小写敏感，且是多字节安全的。

substring_index（“待截取有用部分的字符串”，“截取数据依据的字符”，截取字符的位置N）

## 示例
```mysql
SELECT SUBSTRING_INDEX(‘192,168,8,203’,’,’,1);
# 192
SELECT SUBSTRING_INDEX(‘192,168,8,203’,’,’,-1);
# 203
SELECT SUBSTRING_INDEX(SUBSTRING_INDEX(‘192,168,8,203’,’,’,2),’,’,-1);
# 168
SELECT SUBSTRING_INDEX(SUBSTRING_INDEX(‘192,168,8,203’,’,’,-2),’,’,1);
# 8
SELECT SUBSTRING_INDEX(‘192,168,8,203’,’,’,-1);
# 203
```