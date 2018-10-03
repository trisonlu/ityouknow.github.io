---
layout: post
title: Kafka安装示例
category: other
no-post-nav: true
tags: [MQ]
keywords: MQ,Kafka
excerpt: Kafka入门
---

**下载Kafka**

下载地址：[http://mirrors.tuna.tsinghua.edu.cn/apache/kafka/2.0.0/kafka_2.12-2.0.0.tgz](http://mirrors.tuna.tsinghua.edu.cn/apache/kafka/2.0.0/kafka_2.12-2.0.0.tgz)

**解压Kafka**

```
tar -xzf kafka_2.12-2.0.0.tgz
```

**配置kafka**

进入解压目录config/server.properties
更改点如下：
```
listeners=PLAINTEXT://127.0.0.1:9092
advertised.listeners=PLAINTEXT://127.0.0.1:9092
```

**启动Zookeeper**

```
bin/zookeeper-server-start.sh config/zookeeper.properties 1>/dev/null 2>&1 &
```

**启动Kafka**

```
bin/kafka-server-start.sh config/server.properties 1>/dev/null 2>&1 &
```

**创建Topics**

```
bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test
bin/kafka-topics.sh --list --zookeeper localhost:2181
```

**启动producer**

```
bin/kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic test
输入内容可以被后面启动的consumer接收到
```

**启动consumer**

```
bin/kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic test --from-beginning
```

**测试效果**

生产者
![](https://www.trisonlu.com/assets/images/2018/mq/kafka_producer.png)
消费者
![](https://www.trisonlu.com/assets/images/2018/mq/kafka_consumer.png)

**关闭进程命令**

```
kill -s 9 `ps -aux | grep kafka | awk '{print $2}'`
```
