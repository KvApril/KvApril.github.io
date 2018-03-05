---
layout: post
title: "Ubuntu_sftp和scp命令"
date: 2018-03-03
description: "Ubuntu_sftp和scp命令"
tag: Ubuntu
---
无端口登录

```
$ sftp root@xx.xxx.xx.xx
$ cd /xxx/xx
$ get file_name
```

端口号登录
```
$ sftp -oPort=80 root@xx.xx.xx.xx
$ cd /xxx/xxx
$ get file_name

```

Scp 命令文件

```
$ scp local_file remote_username@remote_ip:remote_folder 
$ scp local_file remote_username@remote_ip:remote_file 
$ scp local_file remote_ip:remote_folder 
$ scp local_file remote_ip:remote_file 

第1,2个指定了用户名，命令执行后需要再输入密码，  
第1个仅指定了远程的目录，文件名字不变，第2个指定了文件名； 
第3,4个没有指定用户名，命令执行后需要输入用户名和密码，  
第3个仅指定了远程的目录，文件名字不变，第4个指定了文件名


```
Scp 复制目录

```
$ scp -r local_folder remote_username@remote_ip:remote_folder 
$ scp -r local_folder remote_ip:remote_folder 
 将本地xxx目录 复制 到 远程xx目录下
```

Scp 从远程复制到本地

```
$ scp -r remote_username@remote_ip:remote_folder local_folder
$ scp remote_username@remote_ip:remote_file local_folder
```

Scp 特定端口

```
$ scp -p 80 remote@xx.xx.xx.xxx:/data/xx  /home/data/
```
