---
lyout: post
title: Kafka系列-Kafka一些常用配置
categories: Kafka系列
description: 大数据之消息中间件
keyword: Kafka
---

#### 一、生产者配置
- buffer.memory : 默认32Mb，客户端缓存消息的大小
-  max.block.ms : 默认60秒，如果在60秒内如果还没有发送消息，则客户端会抛出异常
- Bufferpool : 特定缓存区大小
- acks : 
  - acks = 1 只要分区的leader 副本成功写入消息，那么就会收到来自服务端的成功响应。
  - acks = 0 生产者发送消息后不要等带任务服务端的响应
  - acks = -1 或 all 需要副本都同步成功

#### 二、生产者客户端架构
- 主要有主线程和send 线程
  - 主线程用来创建消息，并且通过拦截器，序列化器，分区其 然后到消息累加器(消息收集器) 都准备好了 send 线程会从累加器中取消息然后经在进行发送

#### 三 kafka 集群
- leader 加 follower
  - leader 负责消息写入等操作，follower 只负责同步
  - hw 和leo
    - hw 最大偏移量
      - 只有同步一致的便宜了，客户端才能消费
  


​

