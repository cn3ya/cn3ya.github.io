---
layout: post
title:  "Spring服务发现:eureka"
date:   2015-09-22 09:41:22
categories: CouldFlare CDN DNS
---

### 概述
在微服务架构中,服务发现是基础

### 术语

### 服务调用

### 高可用
Eureka高可用集群，则可以通过相互注册的方式来实现。Eureka Peer to Peer Communication

### 健康检查(自我保护机制)
如果Eureka Server最近1分钟收到renew的次数小于阈值（即预期的最小值），则会触发自我保护模式，此时Eureka Server此时会认为这是网络问题，它不会注销任何过期的实例。等到最近收到renew的次数大于阈值后，则Eureka Server退出自我保护模式。

| 配置项                                                | 描述               |
|:-----------------------------------------------------|:------------------|
| eureka.server.enable-self-preservation               | 禁用/开启自我保护模式 |
| eureka.server.renewal-percent-threshold              | 自我保护系数        |
| eureka.server.wait-time-in-ms-when-sync-empty        |                   |
| eureka.client.register-with-eureka                   |                   |
| eureka.server.eviction-interval-timer-in-ms          |                   |
| eureka.instance.lease-expiration-duration-in-seconds | 自动删除过期时间阈值    |
| eureka.instance.lease-renewal-interval-in-seconds    | 心跳间隔            |

配置demo
```yml
server:
  port: 10761
spring:
  application:
    name: cloud-registration-center
## eureka ： 主要配置属性在EurekaInstanceConfigBean和EurekaClientConfigBean中
eureka:
  instance:
    # hostname: 127.0.0.1
    # 使用IP注册
    preferIpAddress: true
    # 心跳间隔
    lease-renewal-interval-in-seconds: 3
    # 服务失效时间： 如果多久没有收到请求，则可以删除服务
    lease-expiration-duration-in-seconds: 7
  client:
    # 关闭eureka client
    # enabled: false
    # 注册自身到eureka服务器
    registerWithEureka: true
    # 表示是否从eureka服务器获取注册信息
    fetchRegistry: false
    # 客户端从Eureka Server集群里更新Eureka Server信息的频率
    eureka-service-url-poll-interval-seconds: 60
    # 定义从注册中心获取注册服务的信息
    registry-fetch-interval-seconds: 5
    # 设置eureka服务器所在的地址，查询服务和注册服务都需要依赖这个地址
    serviceUrl:
      defaultZone: http://127.0.0.1:10761/eureka/
       # 设置eureka服务器所在的地址，可以同时向多个服务注册服务
       # defaultZone: http://192.168.21.3:10761/eureka/,http://192.168.21.4:10761/eureka/
  server:
     # renewal-percent-threshold: 0.1
     # 关闭自我保护模式
     enable-self-preservation: false
     # Eureka Server 自我保护系数，当enable-self-preservation=true时，启作用
     # renewal-percent-threshold:
     # 设置清理间隔,单位为毫秒,默认为0
     eviction-interval-timer-in-ms: 3000
     # 设置如果Eureka Server启动时无法从临近Eureka Server节点获取注册信息，它多久不对外提供注册服务
     wait-time-in-ms-when-sync-empty: 6000000
     # 集群之间相互更新节点信息的时间频率
     peer-eureka-nodes-update-interval-ms: 60000
```
### 参考
+ [Spring Cloud技术分析（2）—— 服务治理实践](http://tech.lede.com/2017/03/29/rd/server/SpringCloud1C/)
+ [Understanding Eureka Peer to Peer Communication](https://github.com/Netflix/eureka/wiki/Understanding-Eureka-Peer-to-Peer-Communication)
+ [Spring cloud系列五 Eureka 之集群同步、自我保护模式以及实例注册、心跳、下线](https://blog.csdn.net/hry2015/article/details/78245149)
