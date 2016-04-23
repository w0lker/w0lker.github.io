---
layout: post
title:  "hadoop、kerberos与ldap集成"
date:   2016-02-07
description: "hadoop、kerberos与ldap集成"
tags: hadoop,kerberos,ldap
categories: works
---

### hadoop分配机器角色

center143 namenode

center144 namenode

center145  kdc, slapd, resourcemanager

data140 datanode,nodemanager

data141 datanode,nodemanager

data142 datanode,nodemanager

### 安装kerberos

#### kdc安装，机器center145：
    # 后台kdc服务
    yum install krb5-server
    # 安装kinit等管理工具
    yum install krb5-workstation
    # 安装krb5开发工具
    yum install krb5-devel
    # 安装ldap集成服务
    yum install db4 db4-utils db4-devel cyrus-sasl* krb5-server-ldap -y

#### server安装，机器center144-data140：
    # 客户端库
    yum install krb5-libs
    yum install krb5-workstation
    # 服务机器管理工具，如klogin,kshell,krb5-telnet等等
    yum install krb5-appl-servers
