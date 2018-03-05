---
layout: post
title: "ruby_编译安装ruby时OpenSSL报错"
date: 2018-03-03
description: "ruby_编译安装ruby时OpenSSL报错"
tag: Ruby
---

在编译安装ruby后，替换ruby源是出现下面的报错
```
ERROR:  While executing gem ... (Gem::Exception)

    Unable to require openssl, install OpenSSL and rebuild ruby (preferred) or use non-HTTPS sources
```

### 查看openssl是否安装

```
openssl version

```

### 安装OpenSSL的依赖

```
apt-get install openssl-devel
```

### 重新编译
```
./configure
make
sudo make install
```


2.如果上面的依赖安装不了，尝试

```
虚拟机上的Ubuntu已经安装过openssl但是仍然不能进行openssl编程
尝试执行以下两条命令

sudo apt-get install openssl 
sudo apt-get install libssl-dev
```
