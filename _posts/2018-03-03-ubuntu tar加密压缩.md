---
layout: post
title: "Ubuntu_tar加密压缩"
date: 2018-03-03
description: "Ubuntu_tar加密压缩"
tag: Ubuntu
---

压缩文件

```
touch a.rb
tar -zcf  - a.rb |openssl des3 -salt -k 123456(password) | dd of=a.des3  

```

解压文件

```
dd if=a.des3 |openssl des3 -d -k 123456(password) | tar zxf -  
```
