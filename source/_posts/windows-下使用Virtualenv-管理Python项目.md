---
title: windows 下使用Virtualenv 管理Python项目
date: 2016-05-09 22:57:21
categories: "工具配置"
tags: 
- Virtualenv
- Python
---

### 为什么使用virtualenv ###

我们在使用python时可能会遇到在一台电脑同时装不同的版本Python或者装不同版本的第三方依赖。
这时候就可以用virtualenv来隔绝项目之间第三方依赖。
此外，virtualenv还可以把开发环境打包。一键部署到其他地方。

## windows 环境安装virtualenv ##
**先决条件：**
1. 已经安装Python
2. 已经安装pip或easy_install
<!-- more -->
### 安装virtual ###
（假定按在D:\env文件夹下）
```bash
D:\env> pip install virtualenv
D:\env> pip install virtualenvwrapper
```
### 创建一个虚拟环境 ###
```bash
D:\env> mkvirtualenv env
New python executable in D:\workspace\env1\Scripts\python.exe
Installing setuptools, pip, wheel...done.
```

创建完成后我们可以使用`lsvirtualenv`查看已经创建的虚拟环境

```bash
D:\env>lsvirtualenv

dir /b /ad "D:\env"
========================================
env
```

可以利用`workon 虚拟环境名字`来切环境

### 常用操作 ###

1. 激活虚拟环境 `workon env`
2. 退出虚拟环境`deactivate`
3. 查看当前虚拟环境安装的所有软件包`pip list`

### 结束 ###
那么，愉快的用pip去装各种各样的依赖包吧！
