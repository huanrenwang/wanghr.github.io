---
lyout: post
title: Kafka系列-Kafka基本概念
categories: Kafka系列
description: 大数据之消息中间件
keyword: Kafka
---

#### 一、涉及概念
##### 1.1 分布式与集群的简单介绍

- 什么是分布式
- 什么是集群
- **举例分布式**

![](https://s3.bmp.ovh/imgs/2022/02/165586b7e9bfdfc3.png)
            

- **举例集群**

![](https://s3.bmp.ovh/imgs/2022/02/8e9fa4d52c9490f0.png)
                                    
-
​


- 分布式和集群的区别
   - 它们的存在都是为了如下几个目的
      - 可靠性，可扩展，资源共享，灵活性 。。。。
   - 不同点
      - 分布式可以简单理解为一件事分多个部分完成。
      - 集群多个同样的事情可以让多个部分分别完成。
   - 共同点:
      - 调度
   - 常见问题:
      - 数据安全
         - 数据需要汇总
      - 常见问题场景:
         - 集群数据存缓存



##### 1.2 Kafka 概念

- Kafka是一种高吞吐量的[分布式](https://baike.baidu.com/item/%E5%88%86%E5%B8%83%E5%BC%8F/19276232)发布订阅消息系统 【百度】
- 什么是消息系统？
   - 系统之间的数据常用交互有哪些呢？
      - 接口，消息，同库同表复制【一般不常用，会暴露实现】
      - 什么时候用接口，什么时候用消息系统呢？
         - 一般没有什么特别标准的答案，不过一般实时性较高的功能会用接口
         - 和外系统对接一般用接口【为什么？】
      - 好处【自行百度】，可以记住一个削峰则可。
   - 消息系统
      - 顾名思义 就是把一个系统的数据传输到另一个系统。

      ![](https://s3.bmp.ovh/imgs/2022/02/389a5bfc769248b2.png)



   - kafka 分布式消息系统【下图是一个kafka集群】

![](https://s3.bmp.ovh/imgs/2022/02/b6a02cddd63376e1.png)

   - 涉及概念
      - topic(主题--- 这个翻译不是很好，可以就叫topic)
         - 可以按小区每栋楼前的邮箱柜子理解(消息会发到对应的topic)
      - producer ： 生成者
         - 系统A
         - 系统A1
         - 系统...
      - Consumer:   消费者
         - 系统B
         - 系统B1
         - 系统...
   - Partition: 分区
      - 创建topic 的时候可以指定
      - 一个topic 可以分多个分区
      ![](https://s3.bmp.ovh/imgs/2022/02/2304e8cb7aa775a2.png)

        ![](https://s3.bmp.ovh/imgs/2022/02/76f006ed97c8ce61.png)

        

      - 为啥多分区？
         - 并发写
      - 集群
         - 数据安全性
         - 性能
         - 可扩展
         -  ....
   - Broker:  kakfa 实例，每个Broker 都是集群下的一个实例。
   - 有集群后除了可以提高负载，还能干什么？
      - 数据备份
   - Pub-Sub 流程

![](https://s3.bmp.ovh/imgs/2022/02/92f89a9cd817ae1b.png)


##### 2. Kafka 的基本操作


-  创建新的topic
   -  ./kafka-console-producer.sh --create --bootstrap-server [kafka server 地址]  --replication-factor [num]  --partitions [num] --topic [topicname]
   - 具体可以参考： ./kafka-console-producer.sh --help
- 获取主题
   - ./kafka-topics.sh --list --bootstrap-server localhost:9092
- 发送消息
   - ./kafka-console-producer.sh --bootstrap-server localhost:9092 --topic [topicname] 
- 接收消息
   - ./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic [topicname]
- 备注: 百度的时候会搜到 --zookeeper localhost:2181 的命令，这个是老版本的命令，比较新的kafka 版本不支持了
- 批量发消息
   - kafka-producer-perf-test.sh
      - 参考金琦 ：[https://doc.zeaho.com/pages/viewpage.action?pageId=238206554](https://doc.zeaho.com/pages/viewpage.action?pageId=238206554)
   - 可以自己根据需要自己写
      - java 版

![](https://s3.bmp.ovh/imgs/2022/02/3bda756995fb3744.png)
​


      - Go版

![](https://s3.bmp.ovh/imgs/2022/02/96dee96e3569ea0a.png)


​

