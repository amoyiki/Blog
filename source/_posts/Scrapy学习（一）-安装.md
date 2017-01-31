---
title: Scrapy学习（一） 安装
date: 2017-01-29 17:10:11
categories: "Python"
tags:
- 学习
- Scrapy
---
在开篇之前，不得不吐槽一下，配置Scrapy是我
搞python后配置环境最久的一次了。我赶紧将四小时的配置过程写下来，以免浪费了这些宝贵的踩坑经验。
<!-- more -->
## 安装 ##
在安装Scrapy之前，要先安装相关的依赖模块，否则无论你是手动pip安装还是用IDE（如Pycharm自动安装都会报错
> error: Unable to find vcvarsall.bat

因为pip无法正常的安装一些依赖，所以我们要用wheel来安装。
### 安装wheel及下载.whl文件 ###
> pip install wheel

验证wheel是否正确安装
![image](http://oi6538cys.bkt.clouddn.com/wheel.png)
接下来，下载网上人家编译好的.whl文件
> http://www.lfd.uci.edu/~gohlke/pythonlibs/

用`Ctrl + F`搜索如下文件
> lxml-3.7.2-cp35-cp35m-win_amd64.whl
> pywin32-220.1-cp35-cp35m-win_amd64.whl
> zope.interface-4.3.3-cp35-cp35m-win_amd64.whl
> [pyOpenSSL-16.2.0-py2.py3-none-any.whl](https://pypi.python.org/packages/ac/93/b4cd538d31adacd07f83013860db6b88d78755af1f3fefe68ec22d397e7b/pyOpenSSL-16.2.0-py2.py3-none-any.whl#md5=7c87cf718171f736f29d1becb4c7b7a5)
> Twisted-16.6.0-cp35-cp35m-win_amd64.whl
> Scrapy-1.3.0-py2.py3-none-any.whl 

** 注：** cp后为python版本，我是64位python3.5的版本

最后测试一下安装是否成功
> scrapy startproject myproject
