---
layout: post
title: "Mongodb_去掉默认输出的log"
date: 2018-03-03
description: "Mongodb_查询语句"
tag: Mongodb
--- 
在执行下面连接mongdb代码的时候

```
require 'mongo'
@db = Mongo::Client.new(["localhost:27017"],:database=>'music')
p @db
``` 
 
控制台打印出下面的log

```
 DEBUG -- : MONGODB | Adding localhost:27017 to the cluster.
```

为了不让其打印出来，谷歌之后找到的解决方法： [check it：](http://stackoverflow.com/questions/30292100/how-can-i-disable-mongodb-log-messages-in-console)



```
This logging is coming from the Ruby Mongo driver.   
The default logging level seems to be Logger::DEBUG.  
Change it to something higher to disable the debug output:

Mongo::Logger.logger.level = ::Logger::FATAL
To make the driver log to a logfile instead:

Mongo::Logger.logger       = ::Logger.new('mongo.log')
Mongo::Logger.logger.level = ::Logger::INFO
```

修改后代码：  

```
require 'mongo'
Mongo::Logger.logger.level = ::Logger::FATAL

@db = Mongo::Client.new(["localhost:27017"],:database=>'music')
p @db
```

