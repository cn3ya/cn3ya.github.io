---
layout: post
title:  "Java获取dump文件"
date:   2015-09-22 09:41:22
categories: java generics
---

### 概述
当java内存占用过高，或是内存溢出时。要定位具体有问题的代码通常是分析dump文件。

### 获取dump文件

#### jvm参数
```
-XX:+HeapDumpOnOutOfMemoryError
-XX:HeapDumpPath=/tmp/java_dump_file
```

#### jcmd
```bash
#获取java进程
jcmd -l
#获取dump文件
jcmd <pid> GC.heap_dump <file-path>
```

#### JMX

outputFile: the path of the file for the dump. The file should have the hprof extension
live: if set to true it dumps only the active objects in memory, as we've seen with jmap before

#### Java VisualVM

### 参考
1. [The Java™ Tutorials](https://docs.oracle.com/javase/tutorial/java/generics/types.html)