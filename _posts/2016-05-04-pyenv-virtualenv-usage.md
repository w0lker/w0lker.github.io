---
layout: post
title:  "pyenv和virtualenv使用"
date:   2016-05-04
description: "pyenv和virtualenv使用"
tags: pyenv virtualenv
categories: works
---

### pyenv使用

	# 列出所有的可以安装的工具
	pyenv install --list
	
	# 安装一个版本，如下面安装3.5.1
	pyenv install 3.5.1
	
	# 查看当前使用的python版本
	pyenv version
	
	# 可以显示所有可用的版本
	pyenv versions
	
	# 全局切换版本，如下切换成3.5.1
	pyenv global 3.5.1
	
	# 切换当前目录下使用某个版本，会往本目录写一个文件.python-version，以后使用这个目录都是这个版本
	pyenv local 2.7.11



### pyenv virtualenv使用

	# 创建一个虚拟环境
	pyenv virtualenv 3.5.1 my_env
	
	# 查看所有的虚拟环境
	pyenv virtualenvs
	
	# 进入指定的虚拟环境
	pyenv shell my_env
	
	# 删除指定虚拟环境
	pyenv virtualenv-delete my_env

### 查文档的方式
先使用 pyenv commands查到所有的命令

然后使用 pyenv help commandxxx 来查看命令的说明

### 心得
可以把虚拟环境设置为全局默认的python环境。但是一般不这么干，虚拟环境一般用在一个局部环境，比如某个项目。这样就可以让每个项目有一个自己的python环境，同时可以在自己的环境中安装特定的python依赖。


##### --EOF--

