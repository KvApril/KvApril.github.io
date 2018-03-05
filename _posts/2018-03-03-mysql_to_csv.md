---
layout: post
title: "ruby_将mysql的数据导出到csv文件"
date: 2018-03-03
description: "ruby_将mysql的数据导出到csv文件"
tag: Ruby
---   
将mysql的数据导出，数据格式为csv
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
    def self.upload_data
           CSV.open("test.csv","wb") do |y|
            CnkiNet.limit(100).each do |x|
                y<<[x.user,x.ip,x.mac,x.title]
            end
       end
   end
end
CnkiNet.upload_data
```
