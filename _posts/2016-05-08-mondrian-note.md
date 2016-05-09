---
layout: post
title:  "mondrian教程"
date:   2016-05-08
description: "mondrian教程"
tags: mondrian
categories: works
---

#### mondrian涉及到的概念

* ##### 维

	维是由多个层次(hierarchy)	组成，层次是由级别(level)组成。
	下面这个代码显示了维Gender由一个单一的层组成。单一的层中又有一个叫Gender的级别。
	
		<Dimension name="Gender" foreignKey="customer_id">
			<Hierarchy hasAll="true" primaryKey="customer_id">
				<Table name="t_customer"/>
				<Level name="Gender" column="gender" uniqueMembers="true"/>
			</Hierarchy>
		</Dimension>

	这段代码代表维Gender的值是从表t_customer中取的列gender。因为表t_customer中列gender只用两个值'F'和'M'，因此维Gender只有两个成员：Gender.[F]和Gender.[M]。
	
	

##### --EOF--

