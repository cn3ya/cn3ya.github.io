---
layout: post
title:  "为SVG文件生成字体文件"
date:   2015-09-06 13:21:30
categories: HTML CSS front-end browser
---

###应用场景
在很多前端项目中，我们需要用到第三方字体库像Font-Awesome。并且在大多数情况下我们只使用了很少的一部分，但是却加载了整个字体库文件。所以在这种场景下，我们可以单独提取个别需求的资源内嵌到我们的页面，而不需要引入整个第三方资源库。

###步骤

####1、定位SVG数据在字体库中的位置
分别下载Font-Awesome的CSS文件和SVG文件。接下来，我们以提取`stack-overflow`这个icon为例。
首先打开CSS文件，在编辑器中搜索`stack-overflow`，定位到下面的位置。

![CSS文件](/img/2015-09-06-1.jpg)

可以看到指向SVG文件的`16c`数据。接下来打开SVG文件，搜索`16C`找到下面的`<glyph>`标签，其中`d`属性里面包含有我们需要的数据。

![SVG文件](/img/2015-09-06-2.jpg)

####2、将数据内嵌到HTML文件
需要为`<path>`添加`transform="scale(0.009,-0.009) translate(0,-1536)"`属性，原因请[参考stack overflow](http://stackoverflow.com/questions/18113478/extracting-svg-from-font-awesome){:target="_blank"}。
{% highlight html %}
<svg height="16" width="16">
    <path fill="#828282" transform="scale(0.009,-0.009) translate(0,-1536)" d="M928 135v-151l-707 -1v151zM1169 481v-701l-1 -35v-1h-1132l-35 1h-1v736h121v-618h928v618h120zM241 393l704 -65l-13 -150l-705 65zM309 709l683 -183l-39 -146l-683 183zM472 1058l609 -360l-77 -130l-609 360zM832 1389l398 -585l-124 -85l-399 584zM1285 1536 l121 -697l-149 -26l-121 697z"/>
</svg>
{% endhighlight %}