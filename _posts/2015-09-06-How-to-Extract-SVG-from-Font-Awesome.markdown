---
layout: post
title:  "How to Extract SVG from Font-Awesome"
date:   2015-09-06 13:21:30
categories: HTML CSS front-end browser
---

###Application Scenes
In many front-end prject, there are using third part font like Font-Awesome. And in most case, just very little part of third part resource has been used. So it's the application scenes for extracting SVG data from Font-Awesome and embedding it to our HTML or CSS file.

###Steps

####1、Locate the data in svg file
open Font-Awesome CSS file & SVG file. As a example we search string `stack-overflow` in CSS file and get below, then we find that its content if point to `\f16c`. Next we open SVG file search `16c` and get below, and a `<glyph>` tag contain the data we need.

####2、Embedding the data to our HTML file

{% highlight html %}
<svg height="16" width="16">
    <path fill="#828282" transform="scale(0.009,-0.009) translate(0,-1536)" d="M928 135v-151l-707 -1v151zM1169 481v-701l-1 -35v-1h-1132l-35 1h-1v736h121v-618h928v618h120zM241 393l704 -65l-13 -150l-705 65zM309 709l683 -183l-39 -146l-683 183zM472 1058l609 -360l-77 -130l-609 360zM832 1389l398 -585l-124 -85l-399 584zM1285 1536 l121 -697l-149 -26l-121 697z"/>
</svg>
{% endhighlight %}