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


~~因为生成器在执行函数时，生成器刚被创建，没有接收到yield表达式的值
隐藏当生成器启动时禁止进行无参send()方法~~
### 生产者消费者 ###
```python
def consumer(): # 定义一个消费者，由于有yeild关键字，此方法是个生成器
    print '[Consumer] Init Consumer ...'
    r = 'init ok' # 初始化返回结果，在启动消费者的时候，返回给生成者
    while True:
        n = yield r # 消费者通过yield接收生产者的消息，并返回其结果
        print '[Consumer] consume n = %s, r=%s'%(n,r)
        r = 'consume %s OK' % n # 消费者消费结果，下个循环返回给生成者
def produce(c): # 定义一个生产者，c为消费者生成器
    print '[Producer] Init Producer ...'
    r = c.send(None) # 启动消费者生成器，同时返回第一次结果
    n = 0
    while n < 5:
        n += 1
        print '[Producer] While, Producing %s ...'%n
        r = c.send(n) # 向消费者发送消息并准备接收结果。此时会切换到消费者执行
        print '[Producer] Consumer return: %s'%r
    c.close()
    print '[Producer] Close Producer ....'
```
