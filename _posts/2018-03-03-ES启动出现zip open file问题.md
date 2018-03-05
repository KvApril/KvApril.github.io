---
layout: post
title: "ES_启动出现zip open file问题"
date: 2018-03-03
description: "ES_启动出现zip open file问题"
tag: ElasticSearch
---

ES启动时候出现以下错误信息

```
Exception in thread "main" java.util.zip.ZipException: error in opening zip file
	at java.util.zip.ZipFile.open(Native Method)
	at java.util.zip.ZipFile.<init>(ZipFile.java:220)
	at java.util.zip.ZipFile.<init>(ZipFile.java:150)
	at java.util.jar.JarFile.<init>(JarFile.java:166)
	at java.util.jar.JarFile.<init>(JarFile.java:103)
	at org.elasticsearch.bootstrap.JarHell.checkJarHell(JarHell.java:174)
	at org.elasticsearch.bootstrap.JarHell.checkJarHell(JarHell.java:87)
	at org.elasticsearch.bootstrap.Bootstrap.setup(Bootstrap.java:164)
	at org.elasticsearch.bootstrap.Bootstrap.init(Bootstrap.java:285)
	at org.elasticsearch.bootstrap.Elasticsearch.main(Elasticsearch.java:35)
Refer to the log for complete error details.
```
检查整个解压包，发现tar解压后，文件夹中出现很多隐藏的._xx*文件。多是电脑系统问题
解决方法：
```
1.在bashrc中添加：export COPYFILE_DISABLE=true  
2.在解压的时候添加--exclude="._*"
tar -xzpvf xxxxx.tar --exclude="._*"
```
[discuss.elastic.co](
https://discuss.elastic.co/t/java-util-zip-zipexception/36427
)