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

<!-- more -->

3. 切换命令/图形界面
    
    切换成命令界面（暂时）

    `Ctrl+Alt+空格` `Ctrl+Alt+F1~F6`

    切换成命令模式（永久）
    
    > $>echo "false" | sudo tee /etc/X11/default-display-manager
    
    然后重启Ubuntu

    切换成图形界面（暂时）

    > startx
    
    切换成图形界面（永久）

    > $>echo “/usr/sbin/gdm” | sudo tee /etc/X11/default-display-manager

