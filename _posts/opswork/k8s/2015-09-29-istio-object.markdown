---
layout: post
title:  "istio对象"
date:   2015-09-22 09:41:22
categories: istio
---

### 对象
| 对象     | 说明                 |
|:--------|:--------------------|
| Pilot   | 服务发现,管理envoy代理 |
| Envoy   | 反向代理,负载均衡      |
| Ingress | 入口                 |
| Egress  | 出口                 |

### 路由规则

| 规则             | 说明        |
|:----------------|:-----------|
| VirtualService  | 服务路由规则 |
| DestinationRule | 额外规则     |
| ServiceEntry    | 外部服务     |
| Gateway         | 负载均衡器   |


### 参考
+ [Traffic Management](https://istio.io/docs/concepts/traffic-management/)
