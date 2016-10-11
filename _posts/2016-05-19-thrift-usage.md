---
layout: post
title:  "thrift使用心得"
date:   2016-05-19
description: "thrift使用心得"
tags: thrift usage
categories: works
---

### thrift server比较

* **TThreadedServer**

	TThreadedServer spawns a new thread for each client connection, and each thread remains alive until the client connection is closed. This means that if there are 1000 concurrent client connections, TThreadedServer needs to run 1000 threads simultaneously.

* **TNonblockingServer**

	TNonblockingServer has one thread dedicated for network I/O. The same thread can also process requests, or you can create a separate pool of worker threads for request processing. The server can handle many concurrent connections with a small number of threads since it doesn’t need to spawn a new thread for each connection.

* **TThreadPoolServer (not benchmarked here)**

	TThreadPoolServer is similar to TThreadedServer; each client connection gets its own dedicated server thread. It’s different from TThreadedServer in 2 ways:
Server thread goes back to the thread pool after client closes the connection for reuse. There is a limit on the number of threads. The thread pool won’t grow beyond the limit. Client hangs if there is no more thread available in the thread pool. It’s much more difficult to use compared to the other 2 servers.


##### --EOF--

