---
layout: post
title: "ES_date-histogram extended_bounds"
date: 2018-03-03
description: "ES_date-histogram extended_bounds"
tag: ElasticSearch
---

[参考官方文档](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations-bucket-histogram-aggregation.html#search-aggregations-bucket-histogram-aggregation-extended-bounds)

extended_bounds会强制”直方图聚合” 从指定的最小值 【至】 指定的最大值进行聚合（即使这期间不再有文档）

extended_bounds只有配合min_doc_count:0(强制返回空桶) 才有意义

例子1.format为"yyyy-MM-dd",设置extended_bounds的格式和format相同
```
POST /sales/_search?size=0
{
    "query":{
        "bool":{
            "must":[
                {"range":{"sales_time":{"gte":"2017-03-01T00:30:00Z",lte:"2017-05-01T00:30:00Z"}}}
            ]
        }
    }
    "aggs" : {
        "sales_over_time" : {
            "date_histogram" : {
                "field" : "date",
                "interval" : "1M",
                "format" : "yyyy-MM-dd",
                "min_doc_count" : 0,
                "extended_bounds":{
                    "min":"2017-01-01",
                    "max":"2017-06-01"
                }
            }
        }
    }
}

```


例子2.format为"MM",可知一年月份的数据区间为[1,12],由此设置extended_bounds的区间
```
POST /sales/_search?size=0
{
    "query":{
        "bool":{
            "must":[
                {"range":{"sales_time":{"gte":"2017-03-01T00:30:00Z",lte:"2017-05-01T00:30:00Z"}}}
            ]
        }
    }
    "aggs" : {
        "sales_over_time" : {
            "date_histogram" : {
                "field" : "date",
                "interval" : "1M",
                "format" : "MM",
                "min_doc_count" : 0,
                "extended_bounds":{
                    "min":1,
                    "max":12
                }
            }
        }
    }
}

```
