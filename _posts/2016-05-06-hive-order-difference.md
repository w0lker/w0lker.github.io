---
layout: post
title:  "hive各种排序表达式区别"
date:   2016-05-06
description: "hive各种排序表达式区别"
tags: hive orderby sortby clusterby distributeby
categories: works
---

#### order by
全局排序。

#### sort by
保证每个reduce中有序，只有在只有一个reduce的时候才会是全局有序。

#### distribute by
通过特定的列，然后将该列相同值的行分配到同一个reduce，但是不保证这些行是安装该列的顺序排序。

	FROM (
	  FROM pv_users
	  MAP ( pv_users.userid, pv_users.date )
	  USING 'map_script'
	  AS c1, c2, c3
	  DISTRIBUTE BY c2
	  SORT BY c2, c1) map_output
	INSERT OVERWRITE TABLE pv_users_reduced
	  REDUCE ( map_output.c1, map_output.c2, map_output.c3 )
	  USING 'reduce_script'
	  AS date, count;

Map阶段：从pv_users表中把列userid和date作为map输入，然后使用map_script脚本处理后，变成三列c1,c2,c3。

然后根据c2作为partition键将结果传给reduce处理，并将结果输出为表map_output。

reduce阶段：将map结果的三列通过reduce_script处理后得到date和统计结果并将结果写入表pv_users_reduced

#### cluster by
是distribute by和sort by的结合，既把相同列值的行分配给同一个reduce，同时还能实现按照特定的列进行局部排序。

这个列并不一定是用来分配reduce的那个列，可以是其它列。

使用cluster by的场景都可以使用distribute by和sort by来代替。

	SELECT col1, col2 FROM t1 CLUSTER BY col1
	
	-- 使用distribute by和sort by代替
	
	SELECT col1, col2 FROM t1 DISTRIBUTE BY col1 SORT BY col1 ASC

##### --EOF--
