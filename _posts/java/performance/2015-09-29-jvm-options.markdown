---
layout: post
title:  "JVM常用参数"
date:   2015-09-22 09:41:22
categories: java generics
---

### 概述

Options that begin with -X are non-standard (not guaranteed to be supported on all VM implementations), and are subject to change without notice in subsequent releases of the JDK.
Options that are specified with -XX are not stable and are subject to change without notice.

Boolean options are turned on with -XX:+<option> and turned off with -XX:-<option>.Disa
Numeric options are set with -XX:<option>=<number>. Numbers can include 'm' or 'M' for megabytes, 'k' or 'K' for kilobytes, and 'g' or 'G' for gigabytes (for example, 32k is the same as 32768).
String options are set with -XX:<option>=<string>, are usually used to specify a file, a path, or a list of commands


### 常用参数

#### 环境

| 参数      | 说明     |
|:--------|:-------|
| -client | 客户端    |
| -server | 服务端    |
| -d32    | 32或64位 |

#### 内存

| 参数                            | 说明           |
|---------------------------------|----------------|
| -Xms                            | 开启GC日志     |
| -Xmx                            | 输出详细GC记录 |
| -Xss                            | 输出时间       |
| -XX:MaxHeapFreeRatio            | 输出日期       |
| -XX:MinHeapFreeRatio            | GC日志保存路径 |
| -XX:PermSize                    |                |

#### 异常处理

| 参数                             | 说明           |
|---------------------------------|----------------|
| -XX:+HeapDumpOnOutOfMemoryError |                |
| -XX:HeapDumpPath                |                |
| -XX:+UseGCOverheadLimit         |                |
| -XX:OnOutOfMemoryError          |                |

#### 调试

| 参数                      |说明 |
|:-------------------------|:---|
| -XX:+TraceClassLoading   |    |
| -XX:+TraceClassUnloading |    |
| -Xprof                   |    |
| -Xrunhprof               |    |

### 生产设置参考
```
java \
-server \
-Xms1024m \
-Xmx1024m \
-Xss256k \
-XX:MetaspaceSize=128m \
-XX:MaxMetaspaceSize=128m \
-XX:+DisableExplicitGC \
-Dsun.rmi.dgc.server.gcInterval=3600000 \
-XX:MaxPermSize=128m \
```

### 使用技巧
```bash
#打印所有JVM参数
java \
-server \
-Xms1024m \
-Xmx1024m \
-Xss256k \
-XX:+DisableExplicitGC \
-Dsun.rmi.dgc.server.gcInterval=3600000 \
-XX:MaxPermSize=128m \
-XX:+PrintCommandLineFlags \
-version

#打印所有XX参数
java -XX:+PrintFlagsFinal -version

#打印所有不为默认值的参数
java \
-server \
-Xms1024m \
-Xmx1024m \
-Xss256k \
-XX:+DisableExplicitGC \
-Dsun.rmi.dgc.server.gcInterval=3600000 \
-XX:MaxPermSize=128m \
-XX:+UnlockExperimentalVMOptions \
-XX:+UnlockDiagnosticVMOptions \
-XX:+PrintFlagsFinal \
-version |grep :=

#查看某个进程的JVM参数
jinfo -flags pid

#通过jinfo修改进程JVM参数
```

### 参考

1. [Java HotSpot VM Options](https://www.oracle.com/technetwork/java/javase/tech/vmoptions-jsp-140102.html)
1. [Launches a Java application](https://docs.oracle.com/javase/8/docs/technotes/tools/unix/java.html)
1. [Tuning the Java Runtime System](https://docs.oracle.com/cd/E19683-01/817-2180-10/pt_chap5.html)
