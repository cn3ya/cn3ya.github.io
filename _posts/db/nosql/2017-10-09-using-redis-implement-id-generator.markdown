---
layout: post
title:  "使用redis实现id生成服务"
date:   2017-08-23 13:21:30
categories: db
tags: sql
---

### 背景
在写业务代码时,不想使用过多的try...catch方式处理处理很多系统或依赖的exception

### 实现
注册php全局异常处理函数
{% highlight php %}
set_error_handler()
set_exception_handler()
register_shutdown_function()
{% endhighlight %}
Laravel框架使用`\Illuminate\Foundation\Bootstrap\HandleExceptions`类进行异常管理
{% highlight php %}
public function bootstrap(Application $app)
{
    $this->app = $app;
    error_reporting(-1);
    set_error_handler([$this, 'handleError']);
    set_exception_handler([$this, 'handleException']);
    register_shutdown_function([$this, 'handleShutdown']);
    if (! $app->environment('testing')) {
        ini_set('display_errors', 'Off');
    }
}
{% endhighlight %}
