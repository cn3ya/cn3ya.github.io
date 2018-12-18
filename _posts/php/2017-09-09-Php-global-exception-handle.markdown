---
layout: post
title:  "PHP全局异常处理"
date:   2017-08-23 13:21:30
categories: Laravel
tags: PHP Exception
---

### 背景
在写业务代码时,不想使用过多的try...catch方式处理处理很多系统或依赖的exception

### 实现
注册php全局异常处理函数
```php
set_error_handler()
set_exception_handler()
register_shutdown_function()
```
Laravel框架使用`\Illuminate\Foundation\Bootstrap\HandleExceptions`类进行异常管理
```php
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
```
