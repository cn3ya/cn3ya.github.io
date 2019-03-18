---
layout: post
title:  "Memcached缓存"
date:   2015-09-06 13:21:30
categories: squid cache
---

### 最大值

|    |           |
|:---|:----------|
| 键 | 250 bytes, 部分客户端会自动hash |
| 值 | 默认1M(slab), 通过参数-I来修改    |


### 操作复杂度
O(1)

### 集群

### 持久化
