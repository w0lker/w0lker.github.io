---
layout: post
title:  "线程池和nio的使用场景和原理研究"
date:   2016-05-20
description: "线程池和nio的使用场景和原理研究"
tags: nio thread pool
categories: works
---

### 应用场景比较

io多路复用本身就是为了处理多个连接，而并不是一个连接搞定所有。


IO多路复用主要是为了解决从多个文件描述符fd中获取数据的问题。可以使用的技术是多进程或多线程，但是因为开销大和保护同步区等问题难以简单或高效的解决。因此被引入。

IO多路复用的核心是：维护一张fd表，调用一个函数（如select）阻塞直到其中一个或多个fd有事件（连接、读、写）时返回，接下来扫描该表，并逐一处理其中有事件发生的fd。注意，这个只需要单进程单线程。

现在看题主的问题，假设一个采用该技术的dbserver，使用单线程监听。当有多个数据库的操作过来，也就是发生了多个事件，对于每个事件假设都是向db中写数据，那采用io复用逐一的写入。注意，仍然是单线程的，万一不幸的是第一个fd的写入操作长时间阻塞，这得导致后面多少事件超时啊。

目前的服务器都是使用io多路复用技术来处理多个连接，但注意实际的对这些连接的具体操作主流的方式仍然是异步的。也就是说使用io多路复用获取这些连接，但是并不处理它，而是把它投递到一任务队列中，一个线程池负责处理这个队列。也就是生产者消费者模式。值得注意的是它并不同步处理直到返回。

当然，纯粹用io多路复用处理所有请求而且性能非常好的例子也有——redis。因为它的所有的读写请求都是在内存中操作，不存在阻塞超时，也用不上任务队列+线程池的组合。

一直觉得java的nio这个名字起的特别让人产生混淆。



连接池的建立不是为了提高IO的效率， 而是为了减少内存开销。NIO在高并发读写的时候效率不见得比blocking IO好， 因为硬盘是瓶颈。 NIO的优势是在遇到硬盘IO的时候，如果进程有CPU相关的操作，可以不被阻塞。 这样可以连续发送多个request(后一个request不需要等前一个结束），这个优势在DB的场景下几乎看不到。而且如果所有进程有大量并发读写，那NIO也不会好到哪里去。 



##### --EOF--

