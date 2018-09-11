---
layout: post
title:  "RabbitMQ架构"
date:   2015-09-22 09:41:22
categories: CouldFlare CDN DNS
---

### 概述
RabbitMQ是高性能的消息中间件,合理使用可以实现模块之间的解耦,和提供系统的健壮性

### 术语
RabbitMQ使用 [AMQP协议](https://www.rabbitmq.com/resources/specs/amqp0-9-1.pdf)

|                | 描述      | 类比           |
|:---------------|:---------|:--------------|
| Server(Broker) | 客户端连接 | 信箱(邮差)      |
| vHost          | 虚拟主机   | 公司地址        |
| Exchange       | 路由器    | 公司前台        |
| Queue          | 队列      | 部门           |
| Message        | 消息      | 信件           |
| Binding        | 绑定      | 部门和楼层关系   |
| BindingKey     | 绑定键    |               |
| RoutingKey     | 路由键    |               |
| Producer       | 生产者    | 发件人         |
| Consumer       | 消费者    | 收件人         |
| Channel        | 频道      | 一个包裹多个物件 |

+ Server(broker)：接收客户端连接，实现AMQP消息队列的路由功能的进程.简单来说就是消息队列服务器实体。
+ Vhost：虚拟主机，一个broker里可以开设多个vhost，用作不同用户的权限分离。权限控制组，用户只能关联到一个vhost上，一个vhost中可以有若干个Exchange和Queue，默认的vhost是"/"
+ Exchange：接收生产者发送的消息，并根据Binding规则将消息路由给服务器中的队列 Exchange Type决定了Exchange路由消息额行为，例如，在RabbitMQ中，ExchangeType有Direct、Fanout和Topic三种，不同类型的Exchange路由得到行为是不一样的
+ queue：用于存储还未消费的消息。消息队列载体，每个消息都会被投入到一个或多个队列。
+ Message：由Header和Body组成，Header是由生产者添加到各种属性的集合，包括Message是否被持久化，是由哪个Message Queue接收优先级是多少等，而Body是真正需要传输的APP数据
+ Binding: 绑定，它的作用就是把exchange和queue按照路由规则绑定起来。：
+ BindingKey： 在mq中设置的绑定key
+ Routing Key：路由关键字，exchange根据这个关键字进行消息投递。
+ producer：消息生产者，就是投递消息的程序。
+ consumer：消息消费者，就是接受消息的程序。
+ channel：消息通道，在客户端的每个连接里，可建立多个channel，每个channel代表一个会话任务

### 流程说明
消息队列的使用过程大概如下：
+ （1）客户端（生产者）连接到消息队列服务器，打开一个channel。
+ （2）客户端声明一个exchange，并设置相关属性。
+ （3）客户端声明一个queue，并设置相关属性。
+ （4）客户端使用routing key，在exchange和queue之间建立好绑定关系。
+ （5）客户端投递消息到exchange。
exchange接收到消息后，就根据消息的key和已经设置的binding，进行消息路由，将消息投递到一个或多个队列里。
exchange也有几个类型，完全根据key进行投递的叫做Direct交换机，例如，绑定时设置了routing key为”abc”，那么客户端提交的消息，只有设置了key为”abc”的才会投递到队列。对key进行模式匹配后进行投递的叫做Topic交换机，符号”#”匹配一个或多个词，符号”*”匹配正好一个词。例如”abc.#”匹配”abc.def.ghi”，”abc.*”只匹配”abc.def”。还有一种不需要key的，叫做Fanout交换机，它采取广播模式，一个消息进来时，投递到与该交换机绑定的所有队列。

### Exchange类型

| 类型     | 描述    |
|:--------|:-------|
| Direct  | 键路由  |
| Fanout  | 配置路由 |
| Topic   | 模式路由 |
| Headers | 多键路由 |

#### 1 Direct:
任何发送到Direct Exchange的消息都会被转发到routing_key中指定的Queue
+ 1.一般情况可以使用rabbitMQ自带的Exchange：””(该Exchange的名字为空字符串)；
+ 2.这种模式下不需要将Exchange进行任何绑定(bind)操作；
+ 3.消息传递时需要一个“routing_key”，可以简单的理解为要发送到的队列名字；
+ 4.如果vhost中不存在routing_key中指定的队列名，则该消息会被抛弃。
#### 2 Fanout:
任何发送到Fanout Exchange的消息都会被转发到与该Exchange绑定(Binding)的所有Queue上
+ 1.可以理解为路由表的模式
+ 2.这种模式不需要routing_key
+ 3.这种模式需要提前将Exchange与Queue进行绑定，一个Exchange可以绑定多个Queue，一个Queue可以同多个Exchange进行绑定。
+ 4.如果接受到消息的Exchange没有与任何Queue绑定，则消息会被抛弃。
Demo中创建了一个将一个exchange和一个queue进行fanout类型的bind.但是发送信息时没有用到它，如果要用到它，只要在发送消息时指定该exchange的名称即可，该exchange就会将消息发送到所有和它bind的队列中。在fanout模式下，指定的routing_key是无效的 。
#### 3 Topic:
任何发送到Topic Exchange的消息都会被转发到所有关心routing_key中指定话题的Queue上
+ 1.这种模式较为复杂，简单来说，就是每个队列都有其关心的主题，所有的消息都带有一个“标题”(routing_key)，Exchange会将消息转发到所有关注主题能与routing_key模糊匹配的队列。
+ 2.这种模式需要routing_key，也许要提前绑定Exchange与Queue。
+ 3.在进行绑定时，要提供一个该队列关心的主题，如“#.log.#”表示该队列关心所有涉及log的消息(一个routing_key为”MQ.log.error”的消息会被转发到该队列)。
+ 4.“#”表示0个或若干个关键字，“*”表示一个关键字。如“log.*”能与“log.warn”匹配，无法与“log.warn.timeout”匹配；但是“log.#”能与上述两者匹配。
+ 5.同样，如果Exchange没有发现能够与routing_key匹配的Queue，则会抛弃此消息。
#### 4 Headers:
任何发送到Topic Exchange的消息都会被转发到所有关心routing_key中指定话题的Queue上
+ 1.这种模式较为复杂，简单来说，就是每个队列都有其关心的主题，所有的消息都带有一个“标题”(routing_key)，Exchange会将消息转发到所有关注主题能与routing_key模糊匹配的队列。
+ 2.这种模式需要routing_key，也许要提前绑定Exchange与Queue。
+ 3.在进行绑定时，要提供一个该队列关心的主题，如“#.log.#”表示该队列关心所有涉及log的消息(一个routing_key为”MQ.log.error”的消息会被转发到该队列)。
+ 4.“#”表示0个或若干个关键字，“*”表示一个关键字。如“log.*”能与“log.warn”匹配，无法与“log.warn.timeout”匹配；但是“log.#”能与上述两者匹配。
+ 5.同样，如果Exchange没有发现能够与routing_key匹配的Queue，则会抛弃此消息。


### 参考
1. [AMQP 0-9-1 Model Explained](https://www.rabbitmq.com/tutorials/amqp-concepts.html)
