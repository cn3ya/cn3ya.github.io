---
layout: post
title:  "生成性能测试数据"
date:   2016-10-11 13:21:30
categories: Ruby
---

### 背景
在部署监控系统时,需要生成测试性能数据以验证部署是否成功

### 实现
磁盘,cpu,网络带宽
```
wget -qO- bench.sh | bash
```
进程

TCP连接
```
yum -y install iperf
iperf -s 8000
iperf -c 10.0.2.176 8000 -P 100 -b 1k
```

CPU
```
time $(i=0; while (( i < 9999999 )); do (( i ++ )); done)
```

