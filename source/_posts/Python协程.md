---
title: Python协程
date: 2016-12-16 11:04:21
categories: "Python"
tags:
- 学习
---
 ** -- 施工中 -- **
<!-- more -->

> Because generator-iterators begin execution at the top of the
    generator's function body, there is no yield expression to receive
    a value when the generator has just been created.  Therefore,
    calling send() with a non-None argument is prohibited when the
    generator iterator has just started, and a TypeError is raised if
    this occurs (presumably due to a logic error of some kind).  Thus,
    before you can communicate with a coroutine you must first call
    next() or send(None) to advance its execution to the first yield
    expression.


因为生成器在执行函数时，生成器刚被创建，没有接收到yield表达式的值
隐藏当生成器启动时禁止进行无参send()方法
