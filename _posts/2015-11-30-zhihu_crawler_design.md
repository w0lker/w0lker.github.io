---
layout: post
title:  "从知乎上看到的爬虫架构"
date:   2015-12-30
description: "从知乎上看到的爬虫架构"
tags: 爬虫,架构,调度
categories: works
---

从整体搜索引擎角度，分成三个子系统：爬虫(URL管理和调度下载解析等）、索引(用于全文检索)、存储(解析后的内容和快照等)；

爬虫子系统部分，又分为四个组件：Seeder- > Manager- > Harvester- > Collector(- > Seeder).1) Seeder负责URL管理，也就是定向网站种子url，以及曾经抓过的所有url，可扩展存储网页指纹，历史抓取信息等

2) Manager负责调度，根据你的抓取策略(定时、增量、随机等)从Seeder调取url生成抓取任务；

3) Harvester有多个，竞争得到抓取任务并专心下载，下载后内容传递给Collector;

4) Collector有俩任务，解析html、搜集新链接，并把解析后的内容根据需要传递给索引系统和存储系统，把搜集的新连接传递给Seeder模块。

这个设计是参考了国外一些论文实现的，个人感觉有几个好处：

a) 四个组件组成良性循环，结构清晰，分工和扩展容易；

b) Seeder+Manager 负责长期目标：指定的下载策略控制，根据不同的适用场景可以由不同的算法；

c) Harvester+Collector 负责短期目标：充分发挥计算机资源(CPU/Memory/IO/网络)完成下载和内容解析；

### 几点说明：
1) URL去重可以放到Seeder来做，一个Bloomfilter就行；
2) Harvester网页下载实现可以用一些高效异步IO，比如java的NIO等，单个线程同时发起上千个并发下载没有任何问题；
3) Collecter网页解析主要是个浪费CPU的事情，一般只能开个线程池并发处理，为了提高解析效率，不在乎链接发现很全的情况下，可以考虑正则表达式解析(非常快,推荐);如果是图片的话，Collector就好办了，判断下载完的资源如果是图片，直接到存储系统。
