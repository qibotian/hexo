---
title: 初识RabbitMQ
date: 2020-03-26
categories: ['RabbitMQ']
tags: [QMQP','RabbiTQ']
comments: true
---



<!--more-->

# RabbitMQ 概念

* Server 服务器， 接受客户端请求
* Connection 连接
* Channel 信道，消息读写等操作在信道中进行，一个客户端可以建立多个信道，每个信道代表一个会话任务。
* Message 消息，客户端和服务器之间传送的数据，消息由Properties和Body组成。
* Vitual Host 虚拟主机，用于逻辑隔离。一个虚拟主机里面可以有多干个Exchange和Queue,同一个虚拟主机里面不能有相同的名称Exchange或Queue。
* Exchange 交换机， 接收消息，按照路由规则将消息路由到一个或者多个队列中。常用的交换机类型有 Direct, Topic, Fanout, Headers等四种。
* Bind 绑定。交换机和消息队列的虚拟连接，绑定中可以包含一个或者多个RoutingKey。
* RoutingKey 路由键。
* Queue 消息队列

# rabbitMQ 交换机类型

有四种类型
* Direct
* Topic
* Fanout
* Headers


###


# 队列构造函数含义
```
/**
 * name 队列名称
 * durable 是否持久化， 队列的声明是默认存在内存中，如果rabbitMq重启就会消失，如果想重启之后队列还存在，则开启持久化
 * exclusive 是否独占，
 * autoDelete 是否自动删除，当最后一个消费者断开连接后队列是否自动删除。
 * arguments
    * Message TTL (x-message-ttl): 设置队列中所有消息的生命周期
    * Auto Expire (x-expire): 如果队列在指定时间内没有被访问，就会被删除
    * Max Length(x-max-length):队列的最大长度，如果超过了最大长度，则把最早进入的几条消息删除
    * Dead letter exchange(x-dead-letter-exchange): 当队列中的消息长度大于最大长度，或者过期等，将从队列中删除的消息转发到指定的交换器上。
 */
public Queue(String name, boolean durable, boolean exclusive, boolean autoDelete, Map<String, Object> arguments)

```
