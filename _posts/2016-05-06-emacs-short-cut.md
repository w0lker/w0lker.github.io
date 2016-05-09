---
layout: post
title:  "emacs配置的所有快捷键"
date:   2016-05-06
description: "emacs配置的所有快捷键"
tags: emacs short-cut
categories: works
---

#### 介绍
这个是我的emacs配置的所有快捷键记录。[配置地址](https://github.com/w0lker/emacs.d)

#### 键详细

- 编辑

u undo (来自evil)

C-r redo （来自evil）

- 窗口

C-x o 切换窗口，超过两个窗口显示字母

C-x 2 上下切分成两个window，并且焦点放在刚创建的window，同时新窗口显示其它已经打开的buffer

C-x 3 左右切分成两个window，并且焦点放在刚创建的window，同时新窗口显示其它已经打开的buffer

C-x 1 删除其它窗口，恢复到原来我这一个窗口时的所有状态，适合在一个主窗口中打开很多小窗口看其它东西，然后不需要其它小窗口了，想恢复到只有一个主窗口。如果原来该窗口没有其它配置，则只会删除其它窗口。

C-c left 或者 C-c right  在已经使用过的各种窗口布局之间进行切换。

C-x | 上下切分成两个窗口，不管几个窗口都会变成只有上下两个窗口

C-x _ 左右切分成两个窗口，不管几个窗口都会变成只有两个窗口,可以在C-x |上下布局不满意后直接改成左右布局。很方便的快捷键。

f7 分屏显示最近开口的文档，再按一下会关闭这个分屏。在看文档什么的时候这个快捷键很方便

C-c down 显示当前窗口关联了哪个buffer

- company补全

M-/ 启动补全

M-C-/ 全局的启动补全快捷键



##### --EOF--

