---
layout: post
title: "ES_x-pack Buckets Influencers Records"
date: 2018-03-03
description: "ES_x-pack Buckets Influencers Records"
tag: ElasticSearch
---

[参考官方文档](https://www.elastic.co/guide/en/x-pack/5.x/ml-results-resource.html#ml-results-buckets)

### Buckets
每个job的每个bucket span都会有一个bucket result，每个bucket result都有一个anomaly_score。

如果在一个bucket span中无异常出现，则anomaly_score的结果为0

```
anomaly_score:          任何一个bucket影响者的最大异常得分在0-100之间，这是一个job的整体的，有限的得分。随着新数据被分析，该值会改变
bucket_influencers:     bucket的影响者，影响因素
bucket_span:            bucket的设定长度，在创建job的时候设定
event_count:            在一个bucket中处理的输入数据记录量
initial_anomaly_score:  任何bucket influencers的最大异常得分，这是在bucket进行计算的初始得分
is_interim:             如果是true，这是一个过渡期结果。也就是说bucket results的计算依赖于特定输入的数据
job_id:                 这些结果属于的哪个job的唯一标识符
processing_time_ms:     分析和计算每个bucket所话费的时间（毫秒级）
result_type:            bucket，内部设定
timestamp:              bucketk分析开始的时间，唯一标识了每个bucket

```
