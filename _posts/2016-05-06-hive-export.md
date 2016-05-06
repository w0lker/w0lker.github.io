---
layout: post
title:  "hive数据导出"
date:   2016-05-06
description: "hive数据导出"
tags: hive 导出
categories: works
---

#### 导出到本地
导出到本地可以指定使用什么分隔符的。

	INSERT OVERWRITE LOCAL DIRECTORY '/本地路径' 
	ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' 
	SELECT 查询语句;

没有overwrite表示不覆盖本地的相同的目录下的数据

#### 导出到HDFS
跟导入本地的差别就是没有local,同时不能指定列分割符，默认使用'\001'(^A)作为分割符

	INSERT OVERWRITE DIRECTORY 'hdfs路径' 
	SELECT 查询语句;

#### 导出到其它表

	INSERT OVERWRITE TABLE t_to select * from t_from;

如果不使用overwrite就不覆盖原来的数据

#### 其它一些方法

	# 输出的结果为\t分割
	hive -e 'select 查询语句' >> xxx.txt
	
	hive -f xxx.sql >> xxx.txt


#### 特别注明
pig如果要使用hive的'\001'分割的数据，可以使用'\u001'

##### --EOF--
