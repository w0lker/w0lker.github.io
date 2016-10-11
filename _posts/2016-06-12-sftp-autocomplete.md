---
layout: post
title:  "让sftp支持自动补全"
date:   2016-06-12
description: "让sftp支持自动补全"
tags: sftp autocomplete
categories: works
---

### 方法

    brew install with-readline
    
    # 打开bash配置文件
    vi .bash_profile
    # 添加with-readline支持
    alias sftp='with-readline sftp'
 
 with-readline地址：[http://www.greenend.org.uk/rjk/sw/withreadline.html](http://www.greenend.org.uk/rjk/sw/withreadline.html) 	

##### --EOF--

