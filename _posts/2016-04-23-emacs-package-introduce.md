---
layout: post
title:  "emacs使用包介绍"
date:   2016-04-23
description: "emacs使用包介绍"
tags: 笔记,emacs,diminish,ag,recentf,mmm,subword-mode,multiple-cursors
categories: works
---

#### diminish 
可以让emacs的minor-mode名称变为缩写，这个在minor-mode特别多的时候比较有用，还可以让某些minor-mode不显示

#### ag 
the_silver_searcher搜索代码神器，可以用来替代grep

#### recentf 
记住已经访问过得历史文件，emacs自带

#### mmm 
可以让几个主mode共存

#### subword-mode 
可以让一个单词在定位的时候当多个词定位如:HelloWorld 当成两个词Hello和World

#### multiple-cursors 
可以产生多个选中，并且可以直接一次修改多个选中

#### ido 
对emacs的原生mini-buffer的增强，比如自动补全功能，在mini-buffer下输入敲几下就会自动生成匹配的候选集。还可以使用C-s和C-r在所有缓冲区之间切换，C-x C-d直接浏览当前目录下的目录很方便。一般用这个代替emacs的原生mini-buffer。还有一个helm听说有类似的功能，不过我还没试过。

#### semx
与ido配合着使用，能够让ido对M-x后面的命令也进行自动补全。这样就可以不用记快捷键了

#### flymake
实时语法分析工具

#### flyspell
拼写检查工具

#### guide-key
可以用来在按下某个快捷键前缀后入按下Ctrl键后提示所有以Ctrl开头的快捷键

#### mwe-log-commands
可以显示输入的快捷键，一般在演示代码的时候使用。[使用手册地址](http://melpa.org/#/mwe-log-commands)

#### anzu
非常强大的搜索增强工具，可以让通过C-s或者C-r搜索时显示匹配到的结果数量，以及目前光标所在的匹配位置

#### indent-guide
很好的工具，可以在代码快前显示一个竖线，方便知道代码的层次

#### tramp
可以很方便的在本地编辑远程服务器上的文件，非常推荐。已经集成到新版本的emacs中。[使用手册地址](https://www.emacswiki.org/emacs/TrampMode)

如果有一个远程的开发环境使用这个太方便了。

#### comint
emacs用来处理buffer传过来的命令并且交由指定的处理器去处理的一个代理模块。sql-mode和shell-mode都是基于这个模式的。（Comint mode is a package that defines a general command-interpreter-in-a-buffer. ）[使用手册地址](https://www.emacswiki.org/emacs/ComintMode)

#### winner
winner是一个副模式，激活后可以使用C-c <left> 和C-c <right>来对窗口配置进行redo或者undo。
这样在窗口乱了后可以随时恢复到原来不乱的状态，特别适合使用很多window的场景（emacs中window类似其它编辑器的tab）。

##### --EOF--

