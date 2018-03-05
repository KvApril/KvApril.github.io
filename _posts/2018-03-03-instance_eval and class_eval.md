---
layout: post
title: "ruby_instance_eval and  class_eval"
date: 2018-03-03
description: "关于class_eval 和 instance_eval"
tag: Ruby
--- 
### Object#instance_eval()
instance_eval()方法可以对对象本身self进行操作
```
2.3.3 :009 > a = []
 => []
2.3.3 :011 > a.instance_eval { p self }
[]
 => []
2.3.3 :012 > a.instance_eval { p self.class }
Array
 => Array
2.3.3 :013 > a.instance_eval { self[0] = 1 }
 => 1
2.3.3 :014 > a
 => [1]
```
instance_eval()常用于访问对象的私有数据--特别是实例变量(访问范围是private,只能在类定义内进行赋值/读取等操作。)
```
class A
  def initialize
    @x = 1
  end
end
a = A.new 
a.instance_eval { puts @x } #在类外部访问实例变量
```
instance_eval()中定义方法，生成的是个单例方法
```
obj = Object.new 
obj1 = Object.new
obj.instance_eval do #操作的是obj对象，仅对当前操作的对象创建一个a_method单例方法
  def a_method
    "hola!!"
  end
end
p obj.singleton_methods #[:method]
p obj1.singleton_methods #[]
```

### Module#class_eval()
class_eval 和 module_eval功能类似，可以打开一个类/module，对self对象 和 类进行修改
```
C = Class.new 
C.class_eval do #进入一个类定义体内 创建一个a_method方法
  def a_method
    "hola"
  end
end
c = C.new 
puts c.a_method
```


### 一个元编程中的例子
```
require 'test/unit'
require 'test/unit/ui/console/testrunner'

class FakeTime
  def self.now; 'Mon Apr 06 12:15:50'; end
end

class Loan
  def initialize(book)
    @book = book
    @time = Loan.time_class.now
  end

  def self.time_class #返回一个类
    @time_class || Time
  end

  def to_s
    "#{@book.upcase} loaned on #{@time}"
  end
end

class TestLoan < Test::Unit::TestCase
  def test_to_string
    # Loan.instance_eval{ @time_class = FakeTime } #给类实例(类所私有的)变量@time_class赋值=伪造的时间类
    Loan.class_eval{ @time_class = FakeTime } #给类实例(类所私有的)变量@time_class赋值=伪造的时间类
    loan = Loan.new('war adn pace')
    assert_equal 'WAR ADN PACE loaned on Mon Apr 06 12:15:50',loan.to_s
  end
end

Test::Unit::UI::Console::TestRunner.run(TestLoan)
```
