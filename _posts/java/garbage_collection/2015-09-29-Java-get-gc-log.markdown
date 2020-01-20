---
layout: post
title:  "Java获取GC日志文件"
date:   2015-09-22 09:41:22
categories: java generics
---

### 概述
java内存占用过高，可能是内存溢出或是未做限流等多种原因。要定位具体有问题的代码通常是分析
dump文件，但有的时候发现dump文件正常，并没有GC root丢失的情况。那么在这种情况下，需要
对每次GC的日志记录进行分析。

### 用例

#### jvm参数

| 参数                          | 说明       |
|:-----------------------------|:----------|
| -verbose:gc                  | 开启GC日志  |
| -XX:+PrintGCDetails          | 打印详细信息 |
| -XX:+PrintGCTimeStamps       | 打印时间戳   |
| -XX:+PrintGCDateStamps       | 打印日期     |
| -Xloggc:/path/to/file/gc.log | GC日志存储路径|

#### jstatd监控

### 参考
1. [Verbose Garbage Collection in Java](https://www.baeldung.com/java-verbose-gc)