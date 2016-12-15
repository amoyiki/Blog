---
title: git技巧--gitignore配置
date: 2016-12-15 13:54:08
categories: "Git"
tags:
- git
---
## .gitignore 文件配置 ##
<!-- more -->
<!-- todo -->

### .gitignore 配置无法解决问题时 ###
如果`.gitignore`配置完后，仍无法屏蔽掉特殊文件的情况。我们可以手动修改项目路径下的`.git/info/exclude`文件。例如：
> 在Pycharm下进行Python开发时会生成临时文件`__pycache__/`,只需将这个文件名写到exclude文件内即可。
