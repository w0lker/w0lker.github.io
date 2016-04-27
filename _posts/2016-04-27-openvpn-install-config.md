---
layout: post
title:  "openvpn安装和配置"
date:   2016-04-27
description: "openvpn安装和配置"
tags: openvpn
categories: works
---

### 安装LZO
    wget http://www.oberhumer.com/opensource/lzo/download/lzo-2.06.tar.gz
    tar zxf lzo-2.06.tar.gz
    cd lzo-2.06
    ./configure
    make
    make install

### 安装OpenVPN
下载并且安装
	
	wget http://swupdate.openvpn.org/community/releases/openvpn-2.2.2.tar.gz
	tar zvf openvpn-2.2.2.tar.gz
    cd openvpn-2.2.2
    ./configure # 上面这步可能会提示没有openssl，安装yum install openssl-devel
    make
    make install
    
配置openvpn

- 初始化PIK
    
		mkdir /etc/openvpn
		# 复制生成证书的脚本
	    cp -R easy-rsa /etc/openvpn
	    cd /etc/openvpn/easy-rsa/2.0/
	    # vim vars
	    # 设置最后的正式字段：
	    export KEY_COUNTRY="CN"
	    export KEY_PROVINCE="SH"
	    export KEY_CITY="shanghai"
	    export KEY_ORG="xxxx"
	    export KEY_EMAIL="xxx@xxx.com"
	    export KEY_EMAIL=xxx@xxx.com
	    export KEY_CN=tom
	    export KEY_NAME=tom
	    export KEY_OU=tom
	    export PKCS11_MODULE_PATH=tom
	    export PKCS11_PIN=1234
	    # 使vars设置生效
	    source ./vars
	    # 报错：
	    # No /etc/openvpn/easy-rsa/2.0/openssl.cnf file could be found
	    # Further invocations will fail
	    # 将/etc/openvpn/easy-rsa/2.0目录下的openssl-1.0.0.cnf改名为openssl.cnf可解决：
	    cp openssl-1.0.0.cnf openssl-1.0.0.cnf.bak
	    mv openssl-1.0.0.cnf openssl.cnf
	    # 继续运行脚本设置变量，并清理：
	    source ./vars
	    ./clean-all
	    # 建立私钥
	    ./build-ca
	    # build-ca脚本用于生成一个1024位的RSA私钥，由于前面已经设置过vars文件，直接按回车。

- 建立server key
    
		./build-key-server server
    	# 都回车，最后两个y
    
- 建立client key

		# 和建立server key基本相同，生成的没个客户端证书名字要不同。一份客户端证书对应一个客户端。
		./build-key 使用的用户名
    
    
- 生成Diffie Hellman参数
    
		./build-dh
    
- 将keys目录拷贝到本地

- 创建服务端配置文件
    
		mkdir /etc/openvpn/easy-rsa/2.0/conf/
    	cp ~/openvpn-2.2.2/sample-config-files/server.conf /etc/openvpn/easy-rsa/2.0/conf/

- 编辑配置文件/etc/openvpn/easy-rsa/2.0/conf/server.conf
    
		# 找到：
    	ca ca.crt
    	cert server.crt
    	key server.key
    	dh dh1024.pem
		# 修改为：
    	ca /etc/openvpn/easy-rsa/2.0/keys/ca.crt
    	cert /etc/openvpn/easy-rsa/2.0/keys/server.crt
    	key /etc/openvpn/easy-rsa/2.0/keys/server.key
    	dh /etc/openvpn/easy-rsa/2.0/keys/dh1024.pem
    	# 并将以下几句前的分号去掉，并修改dns为google的dns：
	    proto tcp
	    push "redirect-gateway def1 bypass-dhcp"
	    push "dhcp-option DNS 8.8.8.8"
	    push "dhcp-option DNS 8.8.4.4"
	    client-to-client
	    user nobody
	    group nobody
	    # 给下面这个配置添加;
	    proto udp
    
- 配置内核转发特性
    
		vim /etc/sysctl.conf
    	# 将net.ipv4.ip_forward值改为1
		sysctl -p使配置生效

- 配置iptables转发,请确定网络接口是否为eth0,如果不是要替换

    	-A POSTROUTING -s 10.8.0.0/24 -o eth0 -j MASQUERADE

    	-A INPUT -p udp -m state --state NEW -m udp --dport 1194 -j ACCEPT

    	-A INPUT -p tcp -m state --state NEW -m tcp --dport 1194 -j ACCEPT 

    	-A INPUT -i tun+ -j ACCEPT

	    -A INPUT -s 10.8.0.0/24 -j ACCEPT

	    -A FORWARD -i tun+ -j ACCEPT
    
- 设置开机启动

	    # 拷贝openvpn源码目录sample-scripts下的
	    cp openvpn.init /etc/init.d/openvpn
	    ln -s /etc/openvpn/easy-rsa/2.0/conf/server.conf /etc/openvpn/server.conf
	    service openvpn start
	    chkconfig --add openvpn
	    chkconfig openvpn on
    
- 客户端配置
    
	remote 服务地址 1194
    
	ca 配置下载下来的keys中ca.crt
    
	cert 客户端证书.crt
    
	key 客户端密钥.key


##### --EOF--

