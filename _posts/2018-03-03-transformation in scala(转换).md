---
layout: post
title: "Scala_transformation in scala(转换)"
date: 2018-03-03
description: "Scala_transformation in scala(转换)"
tag: Scala
---

pair RDD:{(1,2),(3,4),(3,6)}

1.方法：reducuByKey(func) 对RDD按key聚合并进行func运算作为新value。



```
rdd.reduceByKey((x,y)=>x+y)  #{(1,2),{3,10}}
```
2.方法：groupByKey()   对RDD按key聚合，新value是聚合的value list
```
rdd.groupByKey()  #{(1,[2]),(3,[4,6])
```
3.方法：mapValues(func) key不变，只对value进行func 操作

```
rdd.mapValues(x=>x+1) #{(1,3),(3,5),(3,7)}
```
4.方法:flatMapValues(func) 针对value进行func操作

```
rdd.flatMapValues(x=>(x to 5)) #{(1,2),(1,3),(1,4),(1,5),(3,4),(3,5)}
```
5.方法：keys() #返回集合的key

```
rdd.keys #{1,3,3}
```
6.方法:values() 返回集合的value

```
rdd.values #{2,4,6}
```
7.方法：sortByKey() 返回根据key进行排序的rdd

```
rdd.sortByKey() #{(1,2),{3,4},(3,6)}
```
8.方法：subtractByKey()

9.方法：join(other) 保留两个rdd共通key对应的记录

```
rdd.join(other rdd) #{(3,(4,9),(3,6,9))} 
```
10.方法：rightOuterJoin(other) 右rdd的所有key都保留

```
rdd.rightOuterJoin(other) #{(3,(Some(4),9),(3,(Some(6),9))}
```
11.方法：leftOuterJoin(other) 左rdd的所有key都保留

```
rdd.leftOuterJoin(other) #{(1,(2,None)),(3,(4,Some(9))),(3,6,Some(9))}
```



