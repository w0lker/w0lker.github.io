---
layout: post
title:  "emacs下rtags安装配置"
date:   2016-07-19
description: "emacs下rtags安装配置"
tags: emacs rtags
categories: works
---

#### 编译安装

1. 安装llvm

    brew install llvm
    
2. 安装rtags
homebrew中的版本不行，需要单独编译

        git clone --recursive https://github.com/Andersbakken/rtags.git
        cd rtags
        mkdir build
        cd build
        LIBCLANG_LLVM_CONFIG_EXECUTABLE=/usr/local/opt/llvm/bin/llvm-config cmake -DCMAKE_INSTALL_PREFIX=/usr/local/rtags ..
        make
        make install
    
3. 启动后台服务

    * 独立启动 
    
            /usr/local/rtags/bin/rdm
    
    * 编写启动脚本
    
            <?xml version="1.0" encoding="UTF-8"?>
            <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
            <plist version="1.0">
              <dict>
                <key>Label</key>
                <string>com.w0lker.rtags.agent</string>
                <key>ProgramArguments</key>
                <array>
                  <string>sh</string>
                  <string>-c</string>
                  <string>/usr/local/rtags/bin/rdm -v --launchd --inactivity-timeout 300 --log-file /Users/tangjun/Library/Logs/rtags.launchd.log</string>
                </array>
            	<key>Sockets</key>
                <dict>
                  <key>Listener</key>
                  <dict>
                	<key>SockPathName</key>
                    <string>/Users/tangjun/.rdm</string>
                  </dict>
                </dict>    
              </dict>
            </plist>

4. emacs中添加配置




##### --EOF--

