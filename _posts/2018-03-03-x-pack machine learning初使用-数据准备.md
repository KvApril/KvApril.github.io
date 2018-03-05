---
layout: post
title: "ES_x-pack machine learning初体验"
date: 2018-03-03

description: "ES_x-pack machine learning初体验"
tag: ElasticSearch
---
### 所需环境

```
Elasticsearch 5.4.1  #存储数据和分析结果
X-Pcak 5.4.1 #包含机器学习功能
Kibana 5.4.1 #提供创建和查看jobs的用户界面
```


### 准备数据
使用官网提供的数据，下载链接

```
https://download.elastic.co/demos/machine_learning/gettingstarted/server_metrics.tar.gz
```
### 解压数据

```
#进入下载目录
tar -zxvf server_metrics.tar.gz
```

### 准备导入数据
1.启动elasticsearch，kibana，创建索引 elastic:changeme 是用户名和密码，根据自己的配置来

```
curl -u elastic:changeme -X PUT -H 'Content-Type: application/json' http://localhost:9200/server-metrics -d '{
   "settings":{
      "number_of_shards":1,
      "number_of_replicas":0
   },
   "mappings":{
      "metric":{
         "properties":{
            "@timestamp":{
               "type":"date"
            },
            "accept":{
               "type":"long"
            },
            "deny":{
               "type":"long"
            },
            "host":{
               "type":"keyword"
            },
            "response":{
               "type":"float"
            },
            "service":{
               "type":"keyword"
            },
            "total":{
               "type":"long"
            }
         }
      }
   }
}'
```

2.导入下载解压后的数据，会导入200MB的数据，server-metrics分成了四个文件导入，_bulk API的数据导入上限是100MB
```
curl -u elastic:changeme -X POST -H "Content-Type: application/json" http://localhost:9200/server-metrics/_bulk --data-binary "@server-metrics_1.json" 

curl -u elastic:changeme -X POST -H "Content-Type: application/json" http://localhost:9200/server-metrics/_bulk --data-binary "@server-metrics_2.json"

curl -u elastic:changeme -X POST -H "Content-Type: application/json" http://localhost:9200/server-metrics/_bulk --data-binary "@server-metrics_3.json"

curl -u elastic:changeme -X POST -H "Content-Type: application/json" http://localhost:9200/server-metrics/_bulk --data-binary "@server-metrics_4.json"
```
3.查看导入的数据
```
curl 'http://localhost:9200/_cat/indices?v' -u elastic:changeme
......
green  open server-metrics                  EEE1i5eiQ8yeAmUTpjrK5w 1 0 905940   0 113.9mb 113.9mb
......
```

### 为这些数据定义索引模式

```
1.登录kibana：http://localhost:5601/
2.点击Management->index Patterns
3.根据向导创建索引模式，如果存在，则新建一个
4.输入server-metrics* 作为索引模式
5.Index contains time-based events选项勾选上
6.从time-filed name list中选择@timestamp
7.点击create生成模式
```

现在就可以在Kibana的机器学习作业中分析这些数据了