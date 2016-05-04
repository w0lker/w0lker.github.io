---
layout: post
title:  "proxychains-ng配置"
date:   2016-05-04
description: "proxychains-ng配置"
tags: proxychains usage
categories: works
---

### 安装
	brew install proxychains-ng

### 配置/usr/local/etc/proxychains.conf
添加本地使用的一个代理服务器

![图1](/images/2016-05-04-proxychains-ng-settings-01.png)

### 注意
在mac 10.11后因为SIP的原因，可能会有一些系统自带的网络命令无法使用，这个时候可以使用brew安装一下其它版本的替代。

##### --EOF--
