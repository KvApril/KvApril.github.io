---
layout: post
title: "rails_whenever gem 使用"
date: 2018-03-03
description: "rails_whenever gem 使用"
tag: Rails
--- 

### 安装gem包

```
$ gem install whenever
或者在Gemfile中添加
gem 'whenever',:require=>false
```

进入项目根目录，生成schedule.rb文件

```
$ wheneverize .
```

### 显示添加的schedule.rb任务

```
$ whenever #不会读取或修改crontab文件
```
### 添加任务
```
$ whenever --update-crontab

```
### 列举所有添加的cron任务
```
$ crontab -l
```

### schedule.rb任务举例
```
every 3.hours do
  runner "MyModel.some_process"
  rake "my:rake:task"
  command "/usr/bin/my_great_command"
end

every 1.day, :at => '4:30 am' do
  runner "MyModel.task_to_run_at_four_thirty_in_the_morning"
end

every :hour do # Many shortcuts available: :hour, :day, :month, :year, :reboot
  runner "SomeModel.ladeeda"
end

every :sunday, :at => '12pm' do # Use any day of the week or :weekend, :weekday
  runner "Task.do_something_great"
end

every '0 0 27-31 * *' do
  command "echo 'you can use raw cron syntax too'"
end

# run this task only on servers with the :app role in Capistrano
# see Capistrano roles section below
every :day, :at => '12:20am', :roles => [:app] do
  rake "app_server:task"
end
```