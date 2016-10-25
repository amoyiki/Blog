---
title: Linux注意事项
date: 2016-05-10 11:41:57
categories: "Linux"
tags:
- 学习
---
1. 下载、解压、执行 `make` `make install` `wget` 等命令需要在命令前加上`sudo`(**PS：最好所有命令都加上**)
2. 解压与压缩命令
    
    解压命令：
    
    - `tar` `-zxvf` *.tar.gz
    - `tar` `-xvf` *.tar
    - `unrar` e *.rar
    - `unzip` *.zip

    压缩命令：
    
    - tar -cf all.tar *.jpg # -c新的包，f文件名
    - tar -rf all.tar *.gif # -r新增加
    
    列出all中所有文件
    
    - tar -tf all.tar 
3. 切换命令/图形界面
    <!-- more -->
    切换成命令界面（暂时）

    `Ctrl+Alt+空格` `Ctrl+Alt+F1~F6`

    切换成命令模式（永久）
    
    > $>echo "false" | sudo tee /etc/X11/default-display-manager
    
    然后重启Ubuntu

    切换成图形界面（暂时）

    > startx
    
    切换成图形界面（永久）

    > $>echo “/usr/sbin/gdm” | sudo tee /etc/X11/default-display-manager

4. Linux 软件安装步骤
    1. 加载配置 `sudo ./configure` **注意：**  在此命令后面添加`--prefix=...`可以指定安装路径，例如`sudo ./configure --prefix=/usr/local/python`
    2. 编译 `sudo make`
    3. 安装 `sudo make install`
5. Linux 清屏命令
    - `$ clear` 保留历史记录，将页面下翻一页而已
    - `$ reset` 真正意义上的清空界面
6. Linux 更改计算机名

    > $ sudo vim /etc/hostname
    > 将第一行改为你想要的名字

7. Ubuntu apt-get update失败
    > E: Could not get lock /var/lib/apt/lists/lock 
    > E: Could not get lock /var/lib/dpkg/lock
    > 将这两个文件删除即可执行update命令

8. 中断命令执行
    > 有时候命令执行到一半发现执行错误，或者命令执行时卡死。需要执行中断命令
    > `Ctrl + z`

9. 创建文件夹或文件
```bash
$> mkdir aa # 创建aa文件夹
$> touch aa.log # 创建aa.log文件(0字节)
```

10 . Linux 查看进程
```bash
ps -ef | grep nginx
>>>>>>> Stashed changes
```
