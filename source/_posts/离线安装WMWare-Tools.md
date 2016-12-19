---
title: 离线安装WMWare Tools
date: 2016-12-19 16:26:33
categories: "工具配置"
tags:
- WMWare
---
[VMWare Tools](http://softwareupdate.vmware.com/cds/vmw-desktop/ws/11.0.0/2305329/windows/packages/)

### 解压tools文件 ###

`win+R`打开运行窗口,解压exe文件
> ..\tools-windows-*.exe /e .\
解压成iso文件
> msiexec /a "..\tools-windows.msi" /qb TARGETDIR=".\"
 
虚拟机加载iso即可安装VMWare Tools
