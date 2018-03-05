---
layout: post
title: "rails_rails g 的时候跳过helper js等文件的生成"
date: 2018-03-03
description: "rails_rails g 的时候跳过helper js等文件的生成"
tag: Rails
--- 

### 全局配置
可以在application.rb中进行配置

```
class Application < Rails::Application
  ...
  config.generators do |cfg|
    cfg.stylesheets     false
    cfg.javascripts     false
    cfg.helpers         false
  end
  
#to skip assets, scaffolds.css, test framework, helpers, view
config.generators do |g|
  g.template_engine nil #to skip views
  g.test_framework  nil #to skip test framework
  g.assets  false
  g.helper false
  g.stylesheets false
end
  
```
这样再进行rails g的时候就会跳过 helper，css，js 文件了 

### 创建controller时单独指定 
或者可以在rails g的时候直接指定

```
rails generate controller home index  --no-helper --no-assets --no-controller-specs --no-view-specs
```
