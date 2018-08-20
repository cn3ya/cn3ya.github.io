---
layout: post
title:  "Laravel生成APP_KEY"
date:   2017-08-17 13:21:30
categories: Laravel
tags: php laravel
---

### 背景
在使用Laravel框架进行项目开发时,需要给不同的环境配置不同的APP_KEY

### 实现
使用laravel框架自带的命令行工具即可生成新的APP_KEY
{% highlight shell %}
> php artisan key:generate
Application key [base64:WP+IVaw7kgmetaMo50QwUQ/soUFBH6Mvq+0hFAxTHVk=] set successfully.
{% endhighlight %}
查看.env配置文件
```
APP_KEY=base64:WP+IVaw7kgmetaMo50QwUQ/soUFBH6Mvq+0hFAxTHVk=
```