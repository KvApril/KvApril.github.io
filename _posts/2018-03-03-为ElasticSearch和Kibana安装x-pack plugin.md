---
layout: post
title: "ES_为ElasticSearch和Kibana安装x-pack插件"
date: 2018-03-03
description: "ES_为ElasticSearch和Kibana安装x-pack插件"
tag: ElasticSearch
---

# 安装es-xpack plugin  
https://www.elastic.co/downloads/x-pack


### 安装X-Pack到elasticsearch
```
进入elasticsearch安装目录
➜  bin ./elasticsearch-plugin install x-pack
-> Downloading x-pack from elastic
[=================================================] 100%
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@     WARNING: plugin requires additional permissions     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
* java.lang.RuntimePermission accessClassInPackage.com.sun.activation.registries
......
......
* javax.net.ssl.SSLPermission setHostnameVerifier
See http://docs.oracle.com/javase/8/docs/technotes/guides/security/permissions.html
for descriptions of what these permissions allow and the associated risks.

Continue with installation? [y/N]y
```
### 安装X-Pack到Kibana
```
进入kibana安装目录
➜  bin/kibana-plugin install x-pack
-> Downloading x-pack from kibana
[=================================================] 100%
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@     WARNING: plugin requires additional permissions     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
* java.lang.RuntimePermission accessClassInPackage.com.sun.activation.registries
......
......
* javax.net.ssl.SSLPermission setHostnameVerifier
See http://docs.oracle.com/javase/8/docs/technotes/guides/security/permissions.html
for descriptions of what these permissions allow and the associated risks.

Continue with installation? [y/N]y


安装之后启动kibana
访问：http://localhost:5601/
默认登录用户名：elastic  
默认登录密码：changeme
```
### 离线安装X-Pack到elasticsearch

```
1.下载x-pack安装包： https://artifacts.elastic.co/downloads/packs/x-pack/x-pack-5.4.0.zip
2.将下载的x-pack-5.4.0放在一个临时文件目录下，注意不要直接放到es的plugins目录下
3.在es安装目录下执行：bin/elasticsearch-plugin install file:///x-pack-zip-path/x-pack-5.4.0.zip

注意ubuntu和mac上file后是三个///
```
### 离线安装X-Pack到Kibana

```
1.下载x-pack安装包： https://artifacts.elastic.co/downloads/packs/x-pack/x-pack-5.4.0.zip
2.在es安装目录下执行：bin/kibana-plugin install file:///x-pack-zip-path/x-pack-5.4.0.zip

注意ubuntu和mac上file后是三个///
```
### 更新X-Pack

```
1.停止elasticsearch
2.卸载x-pack: bin/elasticsearch-plugin remove x-pack
3.安装新版本:bin/elasticsearch-plugin install x-pack

1.停止kibana
2.卸载x-pack: bin/kibana-plugin remove x-pack
3.安装新版本:bin/kibana-plugin install x-pack
```

### 卸载X-Pack

```
1.停止elasticsearch
2.卸载x-pack: bin/elasticsearch-plugin remove x-pack
3.重启elasticsearch

1.停止kibana
2.卸载x-pack: bin/kibana-plugin remove x-pack
3.重启kibana
```


### 安装xpack之后，再次访问集群

```
curl -u elastic 127.0.0.1:9200/_cat/health

初始用户名:elastic
初始密码:changeme
https://www.elastic.co/guide/en/x-pack/current/security-getting-started.html
The default password for the elastic user is changeme


修改elasticsearch,kibana访问的初始密码：
curl -XPUT -u elastic 'localhost:9200/_xpack/security/user/elastic/_password' -H "Content-Type: application/json" -d '{
  "password" : "new_elasticpassword"
}'
curl -XPUT -u elastic 'localhost:9200/_xpack/security/user/kibana/_password' -H "Content-Type: application/json" -d '{
  "password" : "new_kibanapassword"
}'
```

### 编辑elasticsearch.yml 允许匿名请求

```
xpack.security.authc:
  anonymous:
    username: anonymous_user 
    roles: role1, role2 
    authz_exception: true
https://www.elastic.co/guide/en/x-pack/current/anonymous-access.html

```

### X-Pack Role & User
x-pack对es和kibana的保护  
现在创建一个角色(role)和一个用户(user),实现效果：  
1.John Doe能够完全访问匹配events*的索引   
2.对这些索引Johndoe可以在kibana中创建可视化图表和仪表板

```
role: events_admin 
user: johndoe

curl -XPOST -u elastic 'localhost:9200/_xpack/security/role/events_admin' -H "Content-Type: application/json" -d '{
  "indices" : [
    {
      "names" : [ "events*" ],
      "privileges" : [ "all" ]
    },
    {
      "names" : [ ".kibana*" ],
      "privileges" : [ "manage", "read", "index" ]
    }
  ]
}'

curl -XPOST -u elastic 'localhost:9200/_xpack/security/user/johndoe' -H "Content-Type: application/json" -d '{
  "password" : "userpassword",
  "full_name" : "John Doe",
  "email" : "john.doe@anony.mous",
  "roles" : [ "events_admin" ]
}'
```

### x-pack启用邮件身份验证
目的：以验证邮件在传输过程中是否被篡改或损坏

```
➜  bin/x-pack/syskeygen #这会在config/x-pack/下生成一个system_key文件，将其copy到其他节点的相同目录下
Storing generated key in [/Users/weiping/software/elasticsearch-5.4.0/config/x-pack/system_key]...
Ensure the generated key can be read by the user that Elasticsearch runs as, permissions are set to owner read/write only
```

### x-pack启用审核
目的：跟踪Elasticsearch集群尝试和成功的交互

```
#编辑各个节点的elasticsearch.yml添加，重启集群
xpack.security.audit.enabled: true
```

### x-pack破解
x-pack的machine learning模块只能试用一段时间，如果需要破解，可以参考:[http://www.voidcn.com/article/p-wszvlkae-re.html](http://www.voidcn.com/article/p-wszvlkae-re.html)

