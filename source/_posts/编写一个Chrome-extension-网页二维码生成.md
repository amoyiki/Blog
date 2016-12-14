---
title: 编写一个Chrome extension--网页二维码生成
date: 2016-12-13 22:11:33
categories: "Chrome extension"
tags:
---
> 很早之前就想过要用Chrome扩展开发一些实用的，或者有意思扩展。今天在看了`segmentfault`的技术周刊后，决定先按照别人写过的东西去~~抄一遍~~模仿的做一遍。

本篇文章是看了[从小目标开始，编写一个简洁的二维码chrome扩展](https://segmentfault.com/a/1190000007594008)模仿的。这篇文章写得很详细。我主要写写自己模仿过程中的一些问题。
<!-- more -->
## Chrome extension基础 ##
编写Chrome 扩展之前我们需要大致的了解一下Google提供的开发文档。鉴于我可怜的英文水平，我推荐花几分钟看一下下面的文档：
1. [360翻译的官方API文档](http://open.chrome.360.cn/extension_dev/overview.html)
2. [Chrome扩展及应用开发](http://www.ituring.com.cn/minibook/950) ←这本书不仅介绍API用法，还提供了好多实例。


## 编写过程 ##
有了上面几分钟的基础后，我们可以开始正式编写代码了。
1. 首先创建一个文件夹，将扩展所创建的文件都放在里面，方便完成后打包。
2. 首先编写`manifest.json`
这是所有扩展的入口文件。看到后缀我们就知道这文件的语法结构必须符合json的写法。Chrome 扩展必须包含的属性有`name`、`version`、`manifest_version`。其他可选属性包括：`background`、`permissions`、`browser_action`、`page_action`、`options_page`、`content_scripts`等等。
```javascript
{
    //目前Chrome版本为2
    "manifest_version": 2,
    //扩展名称
    "name": "QRcode",
    //扩展版本，可自定义
    "version": "1.0",
    //扩展描述，显示在扩展程序中
    "description": "简洁的二维码生成器",
    //显示在扩展程序中的图标
    "icons": {
        "16": "images/icon16.png",
        "128": "images/icon128.png"
    },
    //权限声明
    "permissions":["tabs"]
}
```
3. 接下来就要编写扩展弹出页面`popup.html`文件。
popup页面在被用户点击时初始化，关闭后就会销毁。所以该页面更多的是用来展示结果的。数据处理则需要`background`这个属性来声明，这里暂时没用到就不多说了。需要注意的是，应该用css指定popup页面大小。另外，Google不允许HTML和JavaScript混写在同一个文件内。所有我们把相应的JS提出来，在HTML中添加外部引用。
```html
<!DOCTYPE html>
<html>
<head>
</head>
<style type="text/css">
    .box {
        height: 200px;
        width: 200px;
        background: #EEE;
    }
    .box .title{
        text-align: center;
        margin-bottom: 10px;
    }
</style>
<body>
<div class="box">
    <div class="title">扫描二维码浏览本页面</div>
    <center>
    <div class="qrcode" id="qrcode"></div>
    </center>
</div>
<script src="js/qrcode.js" type="text/javascript"></script>
<script src="js/popup.js" type="text/javascript"></script>
</body>
</html>
```

4. 编写相应的`popup.js`文件
`chrome.tabs`这个API可以与浏览器的标签页系统进行交互。具体API说明参考[标签--扩展开发文档](http://open.chrome.360.cn/extension_dev/tabs.html)
通过获取到的标签页url传给[QRCode](http://code.ciaoca.com/javascript/qrcode/)。通过`QRCode.js`生成二维码。
```javascript
onload=function(){
  chrome.tabs.getSelected(function(tab){
      //QRCode(元素id,相关配置文件)
      var qrcode = new QRCode("qrcode", {
              text: tab.url,
              width: 160,
              height: 160,
              colorDark : '#000000',
              colorLight : '#ffffff',
              // QRCode的容错级别
              correctLevel : QRCode.CorrectLevel.H
            });
    console.log(qrcode);
  });
}
```
到目前为止，一个简单的QRCode生成器边完成了。
![加载自定义插件](http://github.com/amoyiki/Blog/raw/master/Document/images/chrome_extension_qrcode01.png)
![QRCode](http://github.com/amoyiki/Blog/raw/master/Document/images/chrome_extension_qrcode02.png)

## 后续 ##

如果想让二维码中间位置显示自定义图片(如上图)，那么只需要在popup页面自定义一段CSS即可。
** -- 未完待续 -- **
