---
layout: photo
title: '使用workon时出现workon: command not found错误'
tags:
  - Tool
date: 2019-04-11 22:51:00
categories: Tool
photos:
---
安装了oh-my-zsh，发现workon命令不起作用，报错zsh: command not found: workon
<!--more-->
### 解决方案:
1.编辑.zshrc文件
```bash
sudo vim ~/.zshrc
```
2.在文件最后添加如下代码
```bash
export WORKON_HOME=$HOME/'虚拟环境目录'
source /usr/local/bin/virtualenvwrapper.sh
```
3.让修改生效
```bash
source ~/.zshrc
```



[更多链接](https://www.jianshu.com/p/bba968ca3957)

