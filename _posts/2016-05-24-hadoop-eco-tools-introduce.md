---
layout: post
title:  "hadoop生态系统工具介绍"
date:   2016-05-24
description: "hadoop生态系统工具介绍"
tags: hadoop eco tools
categories: works
---

### Slider
把其他服务部署到yarn中，比如hbase，作为yarn的一个application。

尽管Slider项目的动机是将已存在的应用程序或者服务部署到YARN上，但就YARN本身而言，还不能够很好地驾驭“服务”这种特殊的应用程序，这主要还是由于YARN的以下几个Feature尚未发布，包括：
（1）RM/NM upgrade：RM和NM在升级时，正在运行的服务/Task不能受干扰，当升级完毕后，再重新向他们注册。相关jira：“Work-preserving nodemanager restart”，“Support rolling upgrades in YARN”。
（2）Logs management：服务的log是不断增加的，应该支持滚动递增，相关jira：“Roll up for long-lived services in YARN”
（3）服务注册：服务启动后，应该有一个中央化的服务注册组件，以供服务注册地址，从而让其他访问者发现服务的位置。相关jira：“Add a way to register long-lived services in a YARN cluster”
（4）Container资源可动态伸缩。服务运行过程中，对资源的要求可能会改变，因为，应支持在不停止服务的前提下，对服务的资源动态调整。相关jira：“Support changing resources of an allocated container”
以上只是列举了几个重要的feature，还有其他很多feature待开发。总之，让服务能够灵活的运行在YARN上，让YARN成为一个数据中心的资源管理系统，还有很长一段路要走。


##### --EOF--

