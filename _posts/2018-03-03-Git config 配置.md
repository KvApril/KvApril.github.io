---
layout: post
title: "Git_config配置"
date: 2018-03-03
description: "Git_config配置"
tag: Git
--- 

```
/etc/gitconfig文件：  
系统中对所有用户都普遍适用的配置。若使用 git config 时用--system 选项，读写的就是这个文件。  

~/.gitconfig文件：  
用户目录下的配置文件只适用于该用户。若使用 git config 时用--global 选项，读写的就是这个文件。   

 .git/config文件:  
这里的配置仅仅针对当前项目有效。每一个级别的配置都会覆盖上层的相同配置，所以.git/config 里的配置会覆盖/etc/gitconfig 中的同名变量。
```
### 配置用户信息  

```
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```
第一个要配置的是你个人的用户名称和电子邮件地址。这两条配置很重要，每次 Git 提交时都会引用这两条信息，说明是谁提交了更新，所以会随更新内容一起被永久纳入历史记录

### 查看配置信息

```
$ git config --list     #查看所有已经有的配置项
$ git config user.name  #查看配置的用户名
$ git config user.email
$ git config color.status
$ git config core.ignorecase
```
检测已有的配置信息，其中重复的变量名，意味着配置来自不同的配置文件
