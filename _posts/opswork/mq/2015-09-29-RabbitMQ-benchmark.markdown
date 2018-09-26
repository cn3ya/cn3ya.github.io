---
layout: post
title:  "RabbitMQ基准测试"
date:   2015-09-22 09:41:22
categories: CouldFlare CDN DNS
---

### 实现
```
bin/runjava com.rabbitmq.perf.PerfTest -h amqp://guest:guest@192.168.99.100:5672 -x 1 -y 2 -u "throughput-test-1" -a --id "test 1"
```