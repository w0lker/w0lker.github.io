---
layout: post
title:  "hadoop配置优化"
date:   2016-05-25
description: "hadoop配置优化"
tags: hadoop 配置 优化
categories: works
---

### 文件描述符
因为hdfs在运行的时候会打开很多文件描述符。所以需要配置一个相对较大的系统可允许打开文件描述符数。

* centos
	
		sed -i '$a\fs.file-max = 65535000' /etc/sysctl.conf
		sysctl -p
		
		# 临时生效到重启之前
		sudo ulimit -n 409600
		
		# 持久生效
		sudo sed -i '$a\*    soft    nofile    204800' /etc/security/limits.conf
		sudo sed -i '$a\*    hard    nofile    409600' /etc/security/limits.conf

* ubuntu
	
		sudo sed -i '$a\fs.file-max = 65535000' /etc/sysctl.conf
		sudo sysctl -p

		# hard值一定要大于soft
		sudo sed -i '$a\*    soft    nofile    102400' /etc/security/limits.conf
		sudo sed -i '$a\*    hard    nofile    204800' /etc/security/limits.conf


##### --EOF--

