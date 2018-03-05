---
layout: post
title: "rails_annotate的使用"
date: 2018-03-03
description: "rails_Rack"
tag: Rails
--- 
annotate是一个文档类的gem，可以在model中以注释的方式插入到文件中  
在model注释了表名、字段名、字段类型和约束。

### annotate默认注释 models, tests, fixtures, factories  
  

```
cd /path/to/app
annotate
```

### 仅注释model:
  

```
annotate --exclude tests,fixtures,factories,serializers
```

### 注释路由:
  

```
annotate --routes
```

### 删除 model/test/fixture/factory/serializer 里的注释:
  

```
annotate --delete
```
