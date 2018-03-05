---
layout: post
title: "ruby_线程监控monitor"
date: 2018-03-03
description: "关于ruby线程监控monitor"
tag: Ruby
---   
### 控制线程调度器  

#Thread.stop 停止当前的线程  
#Thread.run  安排运行特定的线程  
#Thread.pass 把当前线程调度出去，允许别的线程  
#Thread.join #Thread.value 挂起调用他们的线程，直到指定的此案城结束为止。  
#下面的程序由于资源竞争(竞态条件) 会引发漫长的等待，程序僵死。

```
class Chaser
  attr_reader :count
  def initialize(name)
    @name = name
    @count = 0
  end
  def chase(other)
    while @count < 5
      while @count - other.count > 1
        Thread.pass
      end
      @count += 1
      print "#{@name}: #{count}\n"
    end
  end
end

c1 = Chaser.new('A')
c2 = Chaser.new('B')
threads = [
  Thread.new{ Thread.stop; c1.chase(c2) },
  Thread.new{ Thread.stop; c2.chase(c1) }
]
start_index = rand(2)
threads[start_index].run
threads[1-start_index].run
threads.each{|t| t.join}
```

### 监视器（Monitor）

```
#互斥  监视器（monitor）
#监视器使用同步函数对包含一些资源的对象进行封装。
class Counter
  attr_reader :count
  def initialize
    @count = 0
  end
  def trick
    @count += 1
  end
end
c = Counter.new
t1 = Thread.new{100_000.times{ c.trick }}
t2 = Thread.new{100_000.times{ c.trick }}
t3 = Thread.new{100_000.times{ c.trick }}
t4 = Thread.new{100_000.times{ c.trick }}
t1.join;t2.join;t3.join;t4.join;p c.count

#monitor
#通过把计数器变成监视器，它获取synchronize方法。对于特定的监视器对象
#每次只有一个县城能够执行synchronize block中的代码。
#因此不会再有两个线程同时缓存中间结果。
require "monitor"
class Counter < Monitor
  attr_reader :count
  def initialize
    @count = 0
    super
  end
  def trick
    synchronize do
      @count += 1
    end
  end
end
c = Counter.new
t1 = Thread.new{1_000_000.times{ c.trick }}
t2 = Thread.new{1_000_000.times{ c.trick }}
t1.join;t2.join; p c.count

#使用mix in .
#把同步放在需要同步的资源里面（当需要对类中所有对象的所有访问进行同步时）
require "monitor"
class Counter
  include MonitorMixin
  attr_reader :count
  def initialize
    @count = 0
    super
  end
  def trick
    synchronize do
      @count += 1
    end
  end
end
c = Counter.new
t1 = Thread.new{1_000_000.times{ c.trick }}
t2 = Thread.new{1_000_000.times{ c.trick }}
t1.join;t2.join; p c.count

#外部监视器，不安全
require "monitor"
class Counter
  attr_reader :count
  def initialize
    @count = 0
    super
  end
  def trick
    synchronize do
      @count += 1
    end
  end
end
c = Counter.new
c.extend(MonitorMixin)
t1 = Thread.new{1_00_000.times{ c.synchronize{ c.trick } }}
t2 = Thread.new{1_00_000.times{ c.synchronize{ c.trick } }}
t1.join;t2.join; p c.count
```
