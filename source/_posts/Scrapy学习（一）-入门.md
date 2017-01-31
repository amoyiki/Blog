---
title: Scrapy学习（二） 入门
date: 2017-01-30 22:12:13
categories: "Python"
tags:
- 学习
- Scrapy
---

## 快速入门 ##
接上篇[Scrapy学习（一） 安装](http://www.amoyiki.com/2017/01/29/Scrapy%E5%AD%A6%E4%B9%A0%EF%BC%88%E4%B8%80%EF%BC%89-%E5%AE%89%E8%A3%85/)，安装后，我们利用一个简单的例子来熟悉如何使用Scrapy创建一个爬虫项目。
<!-- more -->
### 创建一个Scrapy项目 ###
在已配置好的环境下输入
> scrapy startproject dmoz

系统将在当前目录生成一个myproject的项目文件。该文件的目录结构如下
```
dmoz/    # 项目根目录
   scrapy.cfg    # 项目配置文件
   dmoz/    # 项目模块
       __init__.py
        items.py    # 项目item文件，有点类似Django中的模型
        pipelines.py    # 项目pipelines文件，负责数据的操作和存储
        settings.py    # 项目的设置文件.
        spiders/    # 项目spider目录，编写的爬虫脚步都放此目录下
            __init__.py
```
接下来我们以`dmoz.org`为爬取目标。开始变现简单的爬虫项目。
### 编写items ###
在items.py中编写我们所需的数据的模型
```python
from scrapy.item import Item, Field

class Website(Item):
    name = Field()
    description = Field()
    url = Field()
```
这个模型用来填充我们爬取的数据
### 编写Spider ###
在spiders文件下新建爬虫文件。这部分才是业务的核心部分。
首先创建一个继承`scrapy.spiders.Spider`的类
并且定义如下三个属性
- name 标识spider
- start_urls 启动爬虫时进行爬取的url列表，默认为空
- parse() 每个初始的url下载后的response都会传到该方法内，在这个方法里可以对数据进行处理。 
```python
from scrapy.spiders import Spider
from scrapy.selector import Selector

from dirbot.items import Website


class DmozSpider(Spider):
    name = "dmoz"
    allowed_domains = ["dmoz.org"]
    start_urls = [
        "http://www.dmoz.org/Computers/Programming/Languages/Python/Books/",
        "http://www.dmoz.org/Computers/Programming/Languages/Python/Resources/",
    ]

    def parse(self, response):
        sites = response.css('#site-list-content > div.site-item > div.title-and-desc')
        items = []

        for site in sites:
            item = Website()
            item['name'] = site.css(
                'a > div.site-title::text').extract_first().strip()
            item['url'] = site.xpath(
                'a/@href').extract_first().strip()
            item['description'] = site.css(
                'div.site-descr::text').extract_first().strip()
            items.append(item)
        return items
```
其中值得注意的是，在`parse`方法内，我们可以用Selector选择器来提取网站中我们所需的数据。提取的方式有几种。
- xpath() 传入xpath表达式获取节点值
- css() 传入css表达式获取节点值
- re() 传入正则表达式获取节点值 # 此方法本人未测试

### 运行并保存数据 ###
接下来我们运行爬虫，并将爬取的数据存储到json中
> scrapy crawl dmoz -o items.json

### 其他 ###
在运行爬虫的过程中，我遇到了如下报错：
> KeyError: 'Spider not found: dmoz

这个是因为我的spider类中设置的name的值和我`scrapy crawl`运行的spider不一致导致的。

具体代码详见：
[scrapy入门项目](https://github.com/amoyiki/LearnedAndProTest/tree/master/dirbot)
