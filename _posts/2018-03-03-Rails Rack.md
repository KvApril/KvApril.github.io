---
layout: post
title: "rails_Rack"
date: 2018-03-03
description: "rails_Rack"
tag: Rails
--- 

### Rack
Rack 为使用 Ruby 开发的网页程序提供了小型模块化，适应性极高的接口。Rack 尽量使用最简单的方式封装 HTTP 请求和响应，为服务器、框架和二者之间的软件（中间件）提供了统一的 API，只要调用一个简单的方法就能完成一切操作

### rails项目使用中的中间件

```
$ rake middleware
```

### 添加中间件

```
config.middleware.use(new_middleware, args)：把新中间件添加到列表末尾；
config.middleware.insert_before(existing_middleware, new_middleware, args)：在 existing_middleware 之前添加新中间件；
config.middleware.insert_after(existing_middleware, new_middleware, args)：在 existing_middleware 之后添加新中间件；


# config/application.rb
 
# Push Rack::BounceFavicon at the bottom
config.middleware.use Rack::BounceFavicon
 
# Add Lifo::Cache after ActiveRecord::QueryCache.
# Pass { page_cache: false } argument to Lifo::Cache.
config.middleware.insert_after ActiveRecord::QueryCache, Lifo::Cache, page_cache: false
```

config.middleware.swap 可以替换middleware堆栈中的中间件

```
# config/application.rb
 
# Replace ActionDispatch::ShowExceptions with Lifo::ShowExceptions
config.middleware.swap ActionDispatch::ShowExceptions, Lifo::ShowExceptions
```

### 删除中间件

```
config.middleware.delete "Rack::Lock"
```


### 官方示例

```
#my_rack_app.rb
require 'rack'

app = Proc.new do |env|
    ['200',{'Content-Type'=>'text/html'},['A barebones rack app.']]
end

Rack::Handler::WEBrick.run app


运行:ruby my_rack_app.rb
[2017-03-03 15:32:56] INFO  WEBrick 1.3.1
[2017-03-03 15:32:56] INFO  ruby 2.3.3 (2016-11-21) [x86_64-darwin15]
[2017-03-03 15:32:56] INFO  WEBrick::HTTPServer#start: pid=39445 port=8080

访问：http://localhost:8080/
```
