---
title: Nginx学习笔记（一）
date: 2016-10-16 22:42:14
categories: "Nginx"
tags:
- 学习
---
### 在Linux下安装Nginx ###
1.在(Nginx官网)[]上下载压缩包。
2.解压后进行安装
    > 在./configure的时候会报错
    > ./configure: error: the HTTP rewrite module requires the PCRE library.
    >  这时候我们需要在Linux上安装PCRE库
    >  sudo apt-get update
    >  sudo apt-get install libpcre3 libpcre3-dev
    >  再次编译，发现又报了缺少zlib library，我们再次照葫芦画瓢安装zlib
    >  sudo apt-get install zlib1g-dev
    >  再次编译，发现Nginx安装成功！
### Nginx的启动，关闭命令 ###
<!-- more -->

