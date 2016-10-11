---
layout: post
title:  "hadoop的ha接口使用"
date:   2016-05-15
description: "hadoop的ha接口使用"
tags: hadoop ha
categories: works
---

### hdfs的api使用

	Configuration conf = new Configuration();
	conf.set("fs.defaultFS", "hdfs://my-cluster");
	conf.set("dfs.nameservices", "my-cluster");
	conf.set("dfs.ha.namenodes.my-cluster", "nn1,nn2");
	conf.set("dfs.namenode.rpc-address.my-cluster.nn1",
				"xxx1:8020");
	conf.set("dfs.namenode.rpc-address.my-cluster.nn2",
				"xxx2:8020");
	conf.set("dfs.client.failover.proxy.provider.my-cluster",
				"org.apache.hadoop.hdfs.server.namenode.ha.ConfiguredFailoverProxyProvider");
				
	FileSystem fs = null;
	try {
		fs = FileSystem.get(conf);
		FileStatus[] list = fs.listStatus(new Path("/"));
		for (FileStatus file : list) {
			System.out.println(file.getPath().getName());
		}
	} catch (IOException e) {
		e.printStackTrace();
	} finally {
		try {
			fs.close();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}


##### --EOF--

