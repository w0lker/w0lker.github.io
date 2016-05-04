---
layout: post
title:  "homebrew使用"
date:   2016-05-04
description: "homebrew使用"
tags: homebrew usage
categories: works
---

### 术语
formula 表示应用安装方案的定义文件 (The package definition)如：/usr/local/Library/Taps/homebrew/homebrew-core/Formula/foo.rb

keg 表示一个formula的安装目录(The installation prefix of a Formula),如：/usr/local/Cellar/foo/0.1

keg-only 表示一个formula只是被用来在其它项目中依赖的，并不会被直接使用。

Cellar 所有的Kegs都会被安装在这里。(All Kegs are installed here) 如：/usr/local/Cellar

Tap 可选的git的formula或者命令仓库 (An optional Git repository of Formula and/or commands)如：/usr/local/Library/Taps/homebrew/homebrew-versions

Bottle 已经编译好的keg，不用使用源码从头编译。(Pre-built Keg used instead of building from source)如：qt-4.8.4.mavericks.bottle.tar.gz

### 帮助
homebrew最好的文档就是man下的文档，写的很全很明白。

	man brew

### brew link xxx
把某个formula的执行文件链接到/usr/local/bin下

### brew unlink xxx
取消某个formula的链接

### brew upgrade --cleanup
升级同时删除之前安装的那个版本，这个需求我经常需要

### brew cleanup -s xxx
清除特定的formula中的多余安装版本，指定-s会把多余的缓存也给清掉

如果想先不删，只是测试一下可以先使用 brew cleanup --dry-run xxx测试一下看看如果删除到底删哪些。

如果不指定formula就是删除所有的多余的安装版本

### brew command xxx
可以显示命令的执行文件的位置，如：brew command cleanup

### 教程链接
[官方formula教程](https://github.com/Homebrew/brew/blob/master/share/doc/homebrew/Formula-Cookbook.md)



##### --EOF--
