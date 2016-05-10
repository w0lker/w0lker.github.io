---
layout: post
title:  "supervisor使用"
date:   2016-05-10
description: "supervisor使用"
tags: supervisor
categories: works
---

### 介绍
类似于daemontools，可以管理和监控类unix系统上的进程。因为是python写的可移植性比较好。

### 注意
被监控的进程不能是daemon进程

### 标准服务配置
	directory=服务启动的目录
	command=启动的进程
	startsecs=5 ; 启动5秒后没有异常认为正常启动
	stopwaitsecs=0 ; 停止后等待多长时间重启
	autostart=true ; 随supervisord自动启动
	autorestart=true ; 程序退出自动重启
	startretriks=3 ; 启动失败自动重试次数
	user=pcsmaster ; 启动使用的用户
	redirect_stderr=true ; 重定向stderr日志到stdout
	stdout_logfile_maxbytes=20MB
	stdout_logfile_backups=20
	stdout_logfile=/home/pcsmaster/log/binlog-3306.log

### 使用
supervisorctl 后进入控制台,输入help查看帮助


##### --EOF--

