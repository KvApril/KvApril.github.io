---
layout: post
title: "Ubuntu_lsof命令"
date: 2018-03-03
description: "Ubuntu_lsof命令"
tag: Ubuntu
---
```
lsof -i:9200

COMMAND  PID    USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
java    2896 elastic  130u  IPv4  17197      0t0  TCP 114.55.110.46:9200 (LISTEN)
```
lsof输出各列信息的意义如下：

> COMMAND：进程的名称   
> PID：进程标识符  
> USER：进程所有者  
> FD：文件描述符，应用程序通过文件描述符识别该文件。如cwd、txt等 TYPE：文件类型，如DIR、REG等  
> DEVICE：指定磁盘的名称  
> SIZE：文件的大小  
> NODE：索引节点（文件在磁盘上的标识）  
> NAME：打开文件的确切名称

lsof语法格式是：lsof ［options］ filename

```
lsof abc.txt 显示开启文件abc.txt的进程
lsof -c abc 显示abc进程现在打开的文件
lsof -c -p 1234 列出进程号为1234的进程所打开的文件
lsof -g gid 显示归属gid的进程情况
lsof +d /usr/local/ 显示目录下被进程开启的文件
lsof +D /usr/local/ 同上，但是会搜索目录下的目录，时间较长
lsof -d 4 显示使用fd为4的进程
lsof -i 用以显示符合条件的进程情况
lsof -i[46] [protocol][@hostname|hostaddr][:service|port]
  46 --> IPv4 or IPv6
  protocol --> TCP or UDP
  hostname --> Internet host name
  hostaddr --> IPv4地址
  service --> /etc/service中的 service name (可以不止一个)
  port --> 端口号 (可以不止一个)
```

