---
layout: post
title:  "关于java的一些思考"
date:   2016-04-28
description: "关于java的一些思考"
tags: java
categories: works
---


### 关于什么时候使用前置的判断

	String str = xxx;
	if("xxx".equal(str)) {
		xxx;
	}

这样写可以省去str的判空过程

	String str = xxx;
	if(str != null && str.equal("xxx")) {
		xxx;
	}

其它场景还是使用后置好，因为代码的可读性还是非常重要的。

##### --EOF--

