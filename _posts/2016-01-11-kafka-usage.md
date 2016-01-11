---
layout: post
title:  "kafka使用"
date:   2016-01-11
description: "kafka使用"
tags: kafka,使用
categories: works
---

### 创建topic
    kafka-topics.sh --zookeeper pcs2.secoo-inc.com/kafka --create --replication-factor 1 --partition 1 --topic test

### 列出topic
    kafka-topics.sh --zookeeper pcs2.secoo-inc.com/kafka --list

###打开两个中断分别使用下面的两个命令测试发送和接收消息

#### 测试发送消息
    kafka-console-producer.sh --broker-list pcs2.secoo-inc.com:9092 --topic test

#### 测试接收消息
    kafka-console-consumer.sh --zookeeper pcs2.secoo-inc.com/kafka --topic test --from-beginning
