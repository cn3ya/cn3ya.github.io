---
layout: post
title:  "安装谷歌Google Polymer前端框架"
date:   2015-09-18 13:21:30
categories: HTML CSS front-end browser polymer web-component
---

### 背景
所有的web前端页面无非是通过HTML实现页面结构，使用CSS配置样式，编写JavaScript实现程序逻辑。随着产品经理的需求越来越多，应用变得越来越复杂，单纯使用HTML+CSS+JavaScript开发常常有力不从心的感觉。面对这样的挑战，业界有着纷繁多样的解决方案。其中Polymer框架是谷歌基于Web Component理念实现的标准组件框架，Polymer试图解决传统单纯使用HTML+CSS+JavaScript开发复杂应用的挑战。

### Polymer理念

#### 1、页面结构
以往页面结构通常是使用div标签加id来实现，div标签内实现具体类容(其中有着复杂的div嵌套)，id用来区分div是导航栏还是侧栏或是页脚等等。到HTML5添加了几个新标签<header><footer><aside><nav>等等来帮助前端工程师厘清页面结构。而Polymer能实现自定义便签，你可以根据需要将一个页面分成几个部分，并且根据每一个部分的实际作用来命名。

#### 2、CSS样式和JavaScript
