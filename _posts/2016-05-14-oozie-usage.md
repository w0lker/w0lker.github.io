---
layout: post
title:  "oozie使用"
date:   2016-05-14
description: "oozie使用"
tags: oozie usage
categories: works
---

### 时区设置
* 配置oozie-site.xml

		<property>
 			<name>oozie.processing.timezone</name>
 			<value>GMT+0800</value>
		</property>

* 配置启动时间格式为：
		
		start_date=2016-02-15T08:28+0800

* 使用coordinator.xml时timezone属性设置为：
		
		timezone="Asia/Shanghai"

* 配置oozie web的Settings中的为：CST（Asia/Shanghai）

### 报错
	java.lang.IllegalArgumentException: begin > end in range (begin, end):
	
原因分析，主要是集群中有机器的时间不同步的问题。需要使用ntp服务同步所有机器的时间。

### 重新运行coodinate中某个action
	
	# 如运行第9个action
	oozie job -rerun  0000012-160525130141555-oozie-oozi-C -action 9
	
	# 上面重新运行0000012-160525130141555-oozie-oozi-C@9
	
	# 如果有多个action需要重新跑也可以使用9-19这种形式
	oozie job -rerun  0000012-160525130141555-oozie-oozi-C -action 9-19
	
**注意**：重新运行的job是有条件的，状态必须是TIMEDOUT/SUCCEEDED/KILLED/FAILED当中一个。如果不是当中的一个会报错的：
	
	Coord Job Rerun Error: part or all actions are not eligible to rerun!
	
我自己的测试是在TIMEDOUT状态下好像也不能rerun，需要先kill这个action然后再rerun
	
### 动态修改coordinate的配置

	oozie job -change coord_id_xxx  -value concurrency=4

### 在ambria版oozie使用hive过程中出现文件描述符不够问题

This may be related to this [https://issues.apache.org/jira/browse/TEZ-3017](https://issues.apache.org/jira/browse/TEZ-3017)

[https://issues.apache.org/jira/browse/HIVE-12766](https://issues.apache.org/jira/browse/HIVE-12766)

This is fixed in 2.4

Workaround is : Disable ATS.

YARN => Configs => Advanced.

Then search "yarn.timeline-service.enabled", then please uncheck this. After saving changes Ambari will as you to restart related services, then please restart those. Once restarting has been completed, please feel free to stop "App Timeline Server"

### 运行job是使用优先使用用户classpath
	
	 <property>
       <name>oozie.launcher.mapreduce.task.classpath.user.precedence</name>
       <value>true</value>
    </property>  	
  	

##### --EOF--

