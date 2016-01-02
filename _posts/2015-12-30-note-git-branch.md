---
layout: post
title:  "[笔记]git分支操作"
date:   2015-12-30
description: "git分支操作"
tags: git分支
categories: works
---

### git分支操作

#### 查看远程分支
    git branch -a

#### 删除远程分支
    git push origin --delete <branchName>
    git push origin :<branchName>

#### 删除远程tag
    git push origin --delete tag <tagName>
    git push origin :refs/tags/<tagName>

#### 删除没有对应的远程分支的本地分支
    git fetch -p

#### 重命名远程分支

1、删除远程分支

    git push origin --delete <原分支名>

2、重命名本地分支

    git branch -m <原分支名> <新分支名>

3、提交新的分支

    git push origin <新分支>

#### 获取远程tag
    git fetch origin tag <tagName>

#### 提交所有tag
    git push --tags
