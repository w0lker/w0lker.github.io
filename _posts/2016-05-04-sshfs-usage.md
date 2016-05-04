---
layout: post
title:  "sshfs使用"
date:   2016-05-04
description: "sshfs使用"
tags: sshfs usage
categories: works
---

### 安装

	brew install Caskroom/cask/sshfs

### 使用
	sshfs -o allow_other,reconnect,cache=yes 用户名@主机地址:远程目录 本地挂载目录
	# -o的参数有很多，可以通过 man sshfs查看
	

### 错误解决

问题：(process:2435): GLib-CRITICAL **: g_slice_set_config: assertion 'sys_page_size == 0' failed

解决：因为使用的tap是homebrew/fuse/sshfs，有点问题，使用Caskroom/cask/sshfs这个就可以，不会出现上面的错误。

##### --EOF--
