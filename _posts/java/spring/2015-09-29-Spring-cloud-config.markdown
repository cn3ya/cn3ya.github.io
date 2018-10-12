---
layout: post
title:  "SpringCloud配置中心"
date:   2015-09-22 09:41:22
categories: spring aop
---

### 概述
在分布式环境中,集中管理配置能大大简化运维工作

### 服务搭建

### 客户端连接

### 配置更新流程

### 敏感信息保存
#### 1.使用对策加密
添加环境变量
```
ENCRYPT_KEY=mysecret
```
#### 2.使用非对称加密
生成密钥对
```

```
添加配置
```

```
#### 3.加密配置
```bash
#curl -X post http://config-server/encrypt -d plain_text_value
18f131c5e47950ee3c1d961cb24330813b5073b6f2874d103a75fc53645c3726
```
### 参考
+ [Spring Cloud Config](https://cloud.spring.io/spring-cloud-config/single/spring-cloud-config.html)
+ [Spring Cloud Config(中文)](https://springcloud.cc/spring-cloud-config.html)
