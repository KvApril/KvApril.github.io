---
layout: post
title: "rails_passenger配置ruby路径"
date: 2018-03-03
description: "rails_passenger配置ruby路径"
tag: Rails
--- 
### 错误信息
在使用passenger启动rails项目的时候，ruby加载路径出现问题

```
Error details saved to: /tmp/passenger-error-X2IsLX.html
  Message from application: cannot load such file -- bundler/setup (LoadError)
  /usr/lib/ruby/1.9.1/rubygems/custom_require.rb:36:in `require'
  /usr/lib/ruby/1.9.1/rubygems/custom_require.rb:36:in `require'
  /usr/lib/ruby/vendor_ruby/phusion_passenger/loader_shared_helpers.rb:456:in `activate_gem'
  /usr/lib/ruby/vendor_ruby/phusion_passenger/loader_shared_helpers.rb:323:in `block in run_load_path_setup_code'
  /usr/lib/ruby/vendor_ruby/phusion_passenger/loader_shared_helpers.rb:461:in `running_bundler'
  /usr/lib/ruby/vendor_ruby/phusion_passenger/loader_shared_helpers.rb:322:in `run_load_path_setup_code'
  /usr/share/passenger/helper-scripts/rack-preloader.rb:100:in `preload_app'
  /usr/share/passenger/helper-scripts/rack-preloader.rb:156:in `<module:App>'
  /usr/share/passenger/helper-scripts/rack-preloader.rb:30:in `<module:PhusionPassenger>'
  /usr/share/passenger/helper-scripts/rack-preloader.rb:29:in `<main>'
```


### 参考资料

[参考此链接](https://www.phusionpassenger.com/library/config/nginx/reference/#setting_correct_passenger_ruby_value) 

```
which passenger-config
#/opt/passenger/bin/passenger-config


rvm use 2.2.1


/opt/passenger/bin/passenger-config --ruby-command

#passenger-config was invoked through the following Ruby interpreter:
  Command: /usr/local/rvm/wrappers/ruby-1.8.7-p358/ruby
  Version: ruby 1.8.7 (2012-02-08 patchlevel 358) [universal-darwin12.0]
  To use in Apache: PassengerRuby /usr/local/rvm/wrappers/ruby-1.8.7-p358/ruby
  To use in Nginx : passenger_ruby /usr/local/rvm/wrappers/ruby-1.8.7-p358/ruby
  To use with Standalone: /usr/local/rvm/wrappers/ruby-1.8.7-p358/ruby /opt/passenger/bin/passenger start


## Notes for RVM users
Do you want to know which command to use for a different Ruby interpreter? 'rvm use' that Ruby interpreter, then re-run 'passenger-config --ruby-command'.
```

### 问题解决
根据上面方式查找ruby的路径，修改passenger.conf
```
vi passenger.conf

passenger_root /usr/lib/ruby/vendor_ruby/phusion_passenger/locations.ini;
#passenger_ruby /usr/bin/passenger_free_ruby;
passenger_ruby /usr/local/rvm/gems/ruby-2.2.1/wrappers/ruby;
```
