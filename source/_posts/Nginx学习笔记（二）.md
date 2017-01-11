---
title: Nginx学习笔记（二）配置及性能调优
date: 2017-01-06 09:39:42
tags:
---
## 如何使用 ##
### 配置文档 ###
1.nginx文档结构
```nginx
...  #全局块
events { #events块
    ...  
}

http { #http块
    ... #http全局块

    server { #server块
        ... #server全局块

        location [PATTRERN] { #location块
            ...
        }

        location [PATTRERN] {
            ...
        }
    }

    ...
}
```
<!-- more -->
- `全局块`：配置会影响nginx全局指令
- `events块`：配置事件驱动模型和最大连接数
- `http块`：可以嵌套多个server，配置代理，缓存，日志
- `server块`：
- `location块`：
** --施工中-- **
### 性能调优 ###
** --施工中-- **
