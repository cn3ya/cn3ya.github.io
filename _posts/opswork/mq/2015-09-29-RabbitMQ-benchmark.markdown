---
layout: post
title:  "RabbitMQ基准测试"
date:   2015-09-22 09:41:22
categories: CouldFlare CDN DNS
---

### 背景
CouldFlare为个人用户提供了免费的CDN加速服务,只需要将对应的DNS服务器地址配置成CouldFlare提供的地址便能轻松实现网站访问加速

### 需求

### 实现
```
bin/runjava com.rabbitmq.perf.PerfTest -h amqp://guest:guest@192.168.99.100:5672 -x 1 -y 2 -u "throughput-test-1" -a --id "test 1"
```