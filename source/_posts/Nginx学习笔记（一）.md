---
title: Nginx学习笔记（一）
date: 2016-10-16 22:42:14
categories: "Nginx"
tags:
- 学习
---
### 在Linux下安装Nginx ###
1. 在(Nginx官网)[http://nginx.org/en/download.html]上下载压缩包。
2. 解压后进行安装
<!-- more -->

    > 在./configure的时候会报错
    > ./configure: error: the HTTP rewrite module requires the PCRE library.
    >  这时候我们需要在Linux上安装PCRE库
    >  sudo apt-get update
    >  sudo apt-get install libpcre3 libpcre3-dev
    >  再次编译，发现又报了缺少zlib library，我们再次照葫芦画瓢安装zlib
    >  sudo apt-get install zlib1g-dev
    >  再次编译，发现Nginx安装成功！

### Nginx的启动，关闭命令 ###
1. Nginx 启动命令
```shell
/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
```

2. Nginx 关闭命令
```shell
kill -QUIT PID
```

3. 将Nginx写成服务运行
如果每次都去执行`/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf`是非常麻烦的事。所以我们将Nginx的相关操作写成Bash脚本，就能像windows服务一样简单的几个命令就能完成任务。
首先我们在网上Copy一份*[>>Ngnix脚本](http://github.com/amoyiki/Blog/raw/master/Document/nginx)*
然后在Linux执行命令
```shell
$> sudo wget http://github.com/amoyiki/Blog/raw/master/Document/nginx -O /etc/init.d/nginx
$> sudo chmod +x /etc/init.d/nginx
```

现在我们就可以用简短的命令启动服务了

> Usage: /etc/init.d/nginx {start|stop|restart|force-reload|reload|status|configtest|quietupgrade|terminate|destroy}
