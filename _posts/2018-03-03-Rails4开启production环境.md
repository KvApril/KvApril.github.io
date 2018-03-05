---
layout: post
title: "rails4+_生产环境中secret_key_base和assets加载问题"
date: 2018-03-03
description: "rails4_生产环境中secret_key_base和assets加载问题"
tag: Rails
--- 

### secret_key_base 问题
rails4+版本中启动production环境的时候提示：
```
Missing `secret_key_base` for 'production' environment, set this value in `config/secrets.yml`
```

### 原因
```
因为rails 4 出于安全考虑，需要在production 的情况下 ，生成一个key，通过 web_app/config/secrets.yml 读取

production:
  secret_key_base: <%= ENV["SECRET_KEY_BASE"] %>
  
处于安全考虑，此key值不建议放入git
```

### 解决方法
```
1.在服务器上执行 rake secret RAILS_ENV=production 生成key

2.编辑~/.bashrc,添加
export SECRET_KEY_BASE=77cc6867b69965249198ded31d6c346d97

3.执行source ~/.bashrc 使配置生效
```


### 生产环境中assets加载问题

```
在生产环境中assets无法加载

```

### 解决方式
```
编辑config/initializers/assets.rb

Rails.application.config.assets.compile = true 
Rails.application.config.assets.precompile =  ['*.js', '*.css', '*.css.erb'] #需要加载的assets


或者修改environment/production.rb
 config.assets.compile = ture#修改为true
```

最后编译aseets，指定生产环境

```
RAILS_ENV=production bundle exec rake assets:precompile
```

清除编译的文件

```
#in rails 4 or +
bundle exec rake assets:clobber
#in rails 3
bundle exec rake assets:clean
```






