---
layout: post
title:  "jenv使用"
date:   2016-05-04
description: "jenv使用"
tags: jenv 使用
categories: works
---

### 介绍
不用再手动的添加环境变量JAVA_HOME。(jEnv is a command line tool to help you forget how to set the JAVA_HOME environment variable)

### 安装
	brew install jenv

	vim ~/.bash_profile
	
	# 添加内容
	export JENV_ROOT=/usr/local/var/jenv
	if which jenv > /dev/null; then eval "$(jenv init -)"; fi

### 使用

	# 添加java版本
	jenv add /Library/Java/JavaVirtualMachines/jdk1.7.0_80.jdk/Contents/Home
	
	# 列出所有版本
	jenv versions
	
	# 切换版本，如下切换为1.7
	jenv global 1.7
	
	# 切换当前目录下的jdk版本，如切换当前目录下的版本为1.6
	jenv local 1.6
	
	# 查看当前jdk的信心
	jenv info java
	
	# 激活导出JAVA_HOME
	jenv enable-plugin export
	
	# 显示所有的插件
	jenv plugins
	
	# 启动一个版本的shell
	jenv shell 1.6
	
	# 配置maven中的java版本切换
	jenv enable-plugin maven
	

### 查文档的方式
先使用 jenv commands查到所有的命令

然后使用 jenv help commandxxx 来查看命令的说明

[官方网址](http://www.jenv.be/)


##### --EOF--

