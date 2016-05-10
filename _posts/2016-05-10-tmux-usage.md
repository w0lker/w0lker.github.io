---
layout: post
title:  "tmux使用"
date:   2016-05-10
description: "tmux使用"
tags: tmux
categories: works
---

### 配置
	# 设置键前缀
	set -g prefix C-a
	set -g default-terminal "xterm-256color"
	set -sg escape-time 1
	set -g base-index 1
	set -g history-limit 9999
	
	# 使用鼠标，1.9之后版本，之前是set -g mode-mouse on
	# set -g mouse on

	set -g status-left-length 40
	set -g status-right "#(date +%H:%M' ')"
	set -g status-fg colour66
	set -g status-bg colour235
	set -g status-interval 10
	set -g status-attr default
	
	set -g pane-border-fg colour235
	set -g pane-active-border-fg colour240
	set -g display-panes-active-colour colour33
	set -g display-panes-colour colour166
	
	set -g message-bg colour235
	set -g message-fg colour66
	
	setw -g mode-keys vi
	setw -g pane-base-index 1
	setw -g window-status-current-fg colour69
	setw -g window-status-current-bg default
	
	unbind C-b
	bind C-a send-prefix
	bind | split-window -h
	bind - split-window -v
	bind h select-pane -L
	bind j select-pane -D
	bind k select-pane -U
	bind l select-pane -R
	bind -r C-h select-window -t :-
	bind -r C-l select-window -t :+
	bind -r H resize-pane -L 5
	bind -r J resize-pane -D 5
	bind -r K resize-pane -U 5
	bind -r L resize-pane -R 5
	bind -t vi-copy v begin-selection
	bind -t vi-copy y copy-pipe "reattach-to-user-namespace pbcopy"

### 命令模式
	# 类似于vim中
	C-a :
	
### 插件管理
tmux可以使用扩展的插件，最好的方式是使用**[tpm](https://github.com/tmux-plugins/tpm)**插件管理器。

tpm配置比较简单，前提是tmux是**1.9版本**后的:

1. 从github上checkout下项目
	
		git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
	
2. 在~/.tmux.conf中底部添加配置
	
		# List of plugins
		set -g @plugin 'tmux-plugins/tpm'
		set -g @plugin 'tmux-plugins/tmux-sensible'
		
		# Other examples:
		# set -g @plugin 'github_username/plugin_name'
		# set -g @plugin 'git@github.com/user/plugin'
		# set -g @plugin 'git@bitbucket.com/user/plugin'
		
		# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
		run '~/.tmux/plugins/tpm/tpm'	

3. 然后就可以在tmux中使用**prefix + I**执行安装和自动载入啦。还有**prefix + U**更新,**prefix + alt + u**删除不在配置中的插件。

### 关机也可以恢复session
配置~/.tmux.conf：
	
	set -g @plugin 'tmux-plugins/tmux-resurrect'
	set -g @plugin 'tmux-plugins/tmux-continuum'
	
然后通过**prefix + I**安装

具体文档查看github上的两个项目：[tmux-resurrect](https://github.com/tmux-plugins/tmux-resurrect)，[tmux-continuum](https://github.com/tmux-plugins/tmux-continuum)

##### --EOF--

