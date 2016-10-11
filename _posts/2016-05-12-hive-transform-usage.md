---
layout: post
title:  "hive的transform使用"
date:   2016-05-12
description: "hive的transform使用"
tags: hive transform
categories: works
---

### 脚本输入输出
输入：默认每行数据会被处理为按照\t分割的字符串传给用户自定义脚本。空值会被转换为\N,以方便区分值为"NULL"的字符串和真的空串。

输出：也是默认是按照\t分割的字符串输出。空串会被处理为\N,然后按照hive中定义的类型对数据进行转换。

能够通过配置**ROW FORMAT**改变默认行为。

### Debug
调试输出会被输出到hadoop的stderr中。


##### --EOF--

