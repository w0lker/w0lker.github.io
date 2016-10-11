---
layout: post
title:  "linux使用笔记"
date:   2016-05-16
description: "linux使用笔记"
tags: linux usage
categories: works
---

### 查看服务的启动端口
在/etc/services目录下有要启动的服务端口,以查询ntp服务端口为例：

	cat /etc/services|grep ntp


##### --EOF--

