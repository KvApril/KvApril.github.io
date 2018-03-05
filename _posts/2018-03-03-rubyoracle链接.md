---
layout: post
title: "ruby_在rails项目之外操作oracle"
date: 2018-03-03
description: "ruby_在rails项目之外操作oracle"
tag: Ruby
--- 
### 在rails项目之外操作orcale
```
require 'active_record'
require 'kaminari'
require 'oci8'
require 'activerecord-oracle_enhanced-adapter'
require 'json'


#链接数据库配置
CONFIG = {
  self: {
    adapter: "oracle_enhanced",
    database: "//x.x.x:1521/orclrac",
    username: "ajustxx",
    password: "ajustxx"
  },
  other: {
    adapter: "oracle_enhanced",
    database: "(description=(address_list=(address=(protocol=tcp)(host=x.x.x.x)(port=15211)))(connect_data=(sid=wsga2)))",
    username: "bjustxx",
    password: "bjustxx"
  }
}

#model和db的映射
class SelfStu < ActiveRecord::Base;self.establish_connection(CONFIG[:self]);self.table_name = "undergraduate_students";end

#model和db的映射
class OtherStu < ActiveRecord::Base;self.establish_connection(CONFIG[:other]);self.table_name = "undergraduate_students";end


class TableCreate < ActiveRecord::Migration[4.2]
  ActiveRecord::Base.establish_connection(CONFIG[:other])
  #删除表
  def self.delete_tab
      puts "you really want drop all tables? (y|n)"
      a = gets
      return if a.to_s.gsub("\n","") != "y"
    
      puts "sure? (y|n)"
      a = gets
      return if a.to_s.gsub("\n","") != "y"
    
      puts "seriously? (y|n)"
      a = gets
      return if a.to_s.gsub("\n","") != "y"
    
      drop_table :undergraduate_students
  end

  #创建一个表  
  def self.create_tab
      begin
        create_table :undergraduate_students do |t|
          t.string :sno,:limit=>100
          t.string :sname,:limit=>100
        end
        add_index :undergraduate_students, :sno
      rescue Exception => e
        puts e
      end
  end
end
```
