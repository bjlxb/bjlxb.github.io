---
layout: photo
title: Python中格式化json数据并写入文件
tags:
  - Python
date: 2020-05-24 21:06:54
categories: Python
photos:
---
python在写入json文件时，最好对json文件进行格式化，方便阅读。
<!--more-->

在使用json.dump()时设置缩进

- indent: 缩进（一般填4，缩进4格）

- sort_keys: 是否排序（默认False–不排序）

```python
import json

json.dump(file_info, fp, indent=4, sort_keys=True)
```

