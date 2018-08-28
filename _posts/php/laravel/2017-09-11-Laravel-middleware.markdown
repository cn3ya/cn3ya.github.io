---
layout: post
title:  "Laravel中间件"
date:   2017-08-23 13:21:30
categories: Laravel
tags: PHP Laravel Debug
---

### 背景
当业务逻辑变得越来越复杂后,必要的调试信息能快速帮我们定位问题

### 实现
安装debugbar依赖
{% highlight shell %}
composer require barryvdh/laravel-debugbar --dev
{% endhighlight %}
添加middleware将debugbar信息注入到接口输出
{% highlight php %}
class DebugBar
{
    public function handle($request, Closure $next, $guard = null)
    {
        $response = $next($request);
        if ($response instanceof JsonResponse && (env('APP_DEBUG') || $request->input('debug')))
        {
            $debugData = app('debugbar')->getData();
            $debugData['request_parameter'] = $request->input();
            $debugData['cookie'] = $request->cookie();
            $response->setData($response->getData(true) + ['_debugbar' => $debugData]);
        }

        return $response;
    }
}
{% endhighlight %}
修改`\App\Exceptions\Handler`的`render`方法,将debugbar信息注入到接口异常输出
{% highlight php %}
public function render($request, Exception $exception)
{
    if ($exception instanceof RequestException)
    {
        $responseFormat = new ResponseFormat();
        $responseFormat->code = $exception->getCode();
        $responseFormat->msg = $exception->getMessage();
        $response = new JsonResponse($responseFormat);
        if ((env('APP_DEBUG') || $request->input('debug')))
        {
                $debugData = app('debugbar')->getData();
                $debugData['request_parameter'] = $request->input();
                $debugData['cookie'] = $request->cookie();
                $response->setData($response->getData(true) + ['_debugbar' => $debugData]);
        }
        return $response;
    }
    return parent::render($request, $exception);
}
{% endhighlight %}