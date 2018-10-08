---
layout: post
title:  "Spring动作流"
date:   2015-09-22 09:41:22
categories: spring hystrix
---

### 概述
Spring Cloud Stream是用来构建消息驱动的微服务框架,它提供了一系列的配置标准和订阅-消费模型约定.

### 消费者demo
#### 1.添加gradle依赖
```gradle
dependencies {
    compile group: 'org.springframework.cloud', name: 'spring-cloud-starter-stream-rabbit'
}
```
#### 2.代码实现
创建消息实体类Person
```java
public class Person {
    private String name;
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public String toString() {
        return this.name;
    }
}
```
创建spring应用类
```java
@SpringBootApplication
@EnableBinding(Sink.class)
public class ServiceApplication {
    @StreamListener(Sink.INPUT)
    public void handle(Person person) {
        System.out.println("Received: " + person);
    }
}
```
#### 3.运行测试
发布消息
![发布消息](/img/spring_cloud_stream1.png)
打印消息
![打印消息](/img/spring_cloud_stream2.png)
### 参考
+ [Spring Cloud Stream Reference Guide](https://docs.spring.io/spring-cloud-stream/docs/current/reference/htmlsingle/)