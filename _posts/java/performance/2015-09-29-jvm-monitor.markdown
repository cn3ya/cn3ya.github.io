---
layout: post
title:  "JVM命令行工具jcmd"
date:   2015-09-22 09:41:22
categories: java generics
---

### 概述
一站式jvm调试工具

### 使用
获取jvm进程
jcmd

获取命令列表
jcmd pid help

获取VM信息
jcmd pid VM.*

获取Thread信息

获取GC信息

获取JTI信息

### 参考

1. [The jcmd Utility](https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr006.html)
