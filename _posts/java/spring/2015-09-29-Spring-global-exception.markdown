---
layout: post
title:  "Spring全局异常拦截"
date:   2015-09-22 09:41:22
categories: spring exception
---

### 概述
Spring框架是java开发中不可获取的技术,他实现了Ioc容器用来管理bean

### 用例
#### bean绑定
简单理解bean是由容器管理的类
1. 使用`@Bean`可以标记一个方法,该方法返回bean的实例.
2. `@Bean`有`scope`属性用来标识是`单例`绑定还是`原型`绑定.
