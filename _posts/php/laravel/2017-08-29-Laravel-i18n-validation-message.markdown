---
layout: post
title:  "Laravel添加中文校验提示"
date:   2017-08-23 13:21:30
categories: Laravel
tags: PHP Laravel Validation i18n
---

### 背景
Laravel框架默认提供了校验机制,但是框架的默认提示信息是英文的

### 实现
拷贝目录`resources/lang/en`到`resources/lang/cn`,修改文件`resources/lang/cn/validation.php`内容为相应中文提示,即可实现返回中文校验信息
