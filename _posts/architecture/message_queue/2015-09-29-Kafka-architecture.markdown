---
layout: post
title:  "Kafka架构"
date:   2015-09-22 09:41:22
categories: CouldFlare CDN DNS
---

### 概述
Kafka号称是百万级的消息中间件,在日志处理领域有着成功的应用

### 术语

### 性能测试
```
bin/kafka-producer-perf-test.sh \
--topic test_perf \
--num-records 1000000 \
--record-size 1000 \
--throughput 20000 \
--producer-props bootstrap.servers=localhost:9092
```

### 参考
1. [Kafka Documentation](https://kafka.apache.org/documentation/)
