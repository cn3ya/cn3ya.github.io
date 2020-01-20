---
layout: post
title:  "Java获取GC信息"
date:   2015-09-22 09:41:22
categories: java generics
---

### 概述
java内存占用过高，可能是内存溢出或是未做限流等多种原因。要定位具体有问题的代码通常是分析
dump文件，但有的时候发现dump文件正常，并没有GC root丢失的情况。那么在这种情况下，需要
对每次GC的日志记录进行分析。

### 用例

#### 命令行
```bash
jstat -gc pid
jstat -gcutil pid
jstat -gccapacity pid
```

#### jstatd方式
```
jstatd -J-Djava.security.policy=/etc/java/jstatd.all.policy -p 9010
```

#### IDE
在Java VisualVM工具中添加isual GC插件，查看远程jstatd服务器的可视化GC日志

### 参考
1. [The jstat Utility](http://www.hellenico.gr/java/technotes/guides/troubleshoot/tooldescr017.html)
1. [jvmstat 3.0](https://www.oracle.com/technetwork/java/jvmstat-142257.html)