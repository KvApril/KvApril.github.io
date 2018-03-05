---
layout: post
title: "ruby_csv文件数据导入mysql"
date: 2018-03-03
description: "ruby_csv文件数据导入mysql"
tag: Ruby
---   

将csv文件中的数据写入mysql
### 文件操作方式
```
# encoding: utf-8
require 'active_record'
require 'file'
ActiveRecord::Base.establish_connection(
          :adapter   => "mysql",
          :host    => '127.0.0.1',
          :username  => "root",
          :password  => "root",
          :database  => "xibei",
          :encoding  => "utf8" 
  )

class  CnkiNet < ActiveRecord::Base
   def self.load_data
       file  = File.open("results.csv").read
       file.each_line do |line|
          p st = line.split(",")
          user = st[0].to_s
          puts "user: "+user rescue ""
          ip = st[1].to_s
          puts "ip: " + ip rescue ""
          time = st[2].to_s
          puts "time: "+time rescue ""
          mac = st[3].to_s
          puts "mac: "+title rescue ""
          title = st[4].to_s
          puts "title: "+title rescue ""
          puts "----------------------------------------"
       end
   end
end

CnkiNet.load_data
```

### CSV gem
```
# encoding: utf-8
require 'active_record'
require 'csv'
ActiveRecord::Base.establish_connection(
          :adapter   => "mysql",
          :host    => '127.0.0.1',
          :username  => "root",
          :password  => "root",
          :database  => "xibei",
          :encoding  => "utf8" 
  )

class  CnkiNet < ActiveRecord::Base
   def self.load_data
       CSV.foreach("results.csv") do |line|
          puts line
          user = line[0].to_s
          puts "user: "+user rescue ""
          ip = line[1].to_s
          puts "ip: " + ip rescue ""
          time = line[2].to_s
          puts "time: "+time rescue ""
          mac = line[3].to_s
          puts "mac: "+title rescue ""
          title = line[4].to_s
          puts "title: "+title rescue ""

          cnki = CnkiNet.new(:user=>user,:ip=>ip,:time=>time,:mac=>mac,:title=>title)
          cnki.save
          puts "----------------------------------------"
      end
   end
end

CnkiNet.load_data
```