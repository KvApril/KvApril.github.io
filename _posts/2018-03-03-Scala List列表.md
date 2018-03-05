---
layout: post
title: "Scala_List"
date: 2018-03-03
description: "Scala_List"
tag: Scala
--- 
Scala列表类似数组，列表是不可变的，数组是可变的，列表具有递归结构(链表结构)，数组无  
生成列表

```
//字符串列表
val site :List[String] = List("runoob","google","baidu")// site: List[String] = List(runoob, google, baidu)
//整形列表
val num :List[Int] = List(1,2,3,4)// num: List[Int] = List(1, 2, 3, 4)
//空列表
val empty :List[Nothing] = List()
//二维列表
val dim :List[List[Int]] = List(
    List(1,2,3),
    List(4,5,6),
    List(7,8,9)
)// dim: List[List[Int]] = List(List(1, 2, 3), List(4, 5, 6), List(7, 8, 9))


val site = "runoob"::("google"::("baidu"::Nil))
val num = 1::(2::(3::(4::Nil)))
val empty = Nil
val dim = (1::(2::(3::Nil)))::(4::(5::(6::Nil)))::(7::(8::(9::Nil)))

```
方法：  
head 获取列表第一个元素  
tail 获取列表最后一个元素
isEmpty:判断列表是否为空

```
site.head // res7: String = runoob
num.head // res9: Int = 1
empty.head //error
dim.head // res12: Any = List(1, 2, 3)

site.tail // res7: String = baidu
num.tail // res9: Int = 3
empty.head //error
dim.tail //res12: Any = List(7, 8, 9)

site.isEmpty // res13: Boolean = false
empty.isEmpty //res14: Boolean = true


```
连接列表：  
List.:::()    
List.concat()  
:::

```
site.:::(num)// resxx: List[Any] = List(runoob, google, baidu, 1, 2, 3, 4)
site:::num// resxx: List[Any] = List(runoob, google, baidu, 1, 2, 3, 4)
List.concat(site,num)// resxx: List[Any] = List(runoob, google, baidu, 1, 2, 3, 4)
```

创建一个指定重复数量元素的列表  
List.fill()
```
val site = List.fill(5)("runoob")// site: List[String] = List(runoob, runoob, runoob, runoob, runoob)
val num = List.fill(10)(123)// num: List[Int] = List(123, 123, 123, 123, 123)

```

通过给定函数来创建列表  
List.tabulate()

```
val seq = List.tabulate(6)(n=>n*n)// seq: List[Int] = List(0, 1, 4, 9, 16, 25)
val seq = List.tabulate(6)(_*_) // seq: List[Int] = List(0, 1, 4, 9, 16, 25)
val seq = List.tabulate(6)(_+2) //seq: List[Int] = List(2, 3, 4, 5, 6, 7)

val seq = List.tabulate(4,5)(_+_)// seq: List[List[Int]] = List(List(0, 1, 2, 3, 4), List(1, 2, 3, 4, 5), List(2, 3, 4, 5, 6), List(3, 4, 5, 6, 7))



```
将列表的顺序反转  
List.reverse

```
val site = "Runoob" :: ("Google" :: ("Baidu" :: Nil)) // site: List[String] = List(Runoob, Google, Baidu)
site.reverse // res23: List[String] = List(Baidu, Google, Runoob)

```

为列表预添加元素  
def +:(elem:A) :List[A]
```
val x = List(1,2,3)// x: List[Int] = List(1, 2, 3)
val y = 56 +: x // y: List[Int] = List(56, 1, 2, 3)
val y = "ss" +: x// y: List[Any] = List(ss, 1, 2, 3)
println(x)// List(1, 2, 3) +:不会改变原有列表
```
为列表开头添加元素  
def ::(x:A) :List[A] 
```
val x = List(1,2,3)// x: List[Int] = List(1, 2, 3)
5 :: x # res26: List[Int] = List(5, 1, 2, 3)
x // res27: List[Int] = List(1, 2, 3)

```
在列表开头添加指定列表的元素  
def :::(prefix :List[A]) :List[A]
```
val x = List(1,2,3)// x: List[Int] = List(1, 2, 3)
val y = x ::: List(4,5,6)//y: List[Int] = List(1, 2, 3, 4, 5, 6)
val z = List(4,5,6) ::: x//z: List[Int] = List(4, 5, 6, 1, 2, 3)
x //res33: List[Int] = List(1, 2, 3)

```
复制添加元素后的列表  
def :+(elem:A) :List[A]
```
val a = List(1,2,3)// a: List[Int] = List(1, 2, 3)
val b = a :+ 77 // b: List[Int] = List(1, 2, 3, 77)

a //res34: List[Int] = List(1, 2, 3)

```
通过列表索引获取元素  
def apply(n :Int) : A
```
val x = List(1,2,3,4,5,6,7)//x: List[Int] = List(1, 2, 3, 4, 5, 6, 7)
x.apply(5)//res36: Int = 6

```

检测列表是否包含指定的元素  
def contains(elem :Any) :Boolean
```
val ss = List("rooo","gooo","booo")//ss: List[String] = List(rooo, gooo, booo)
ss.contains("rooo")//res37: Boolean = true
ss.contains("roo")//res38: Boolean = false

```
将列表的元素复制到数组中  
def copyToArray(xs:Array[A],start:Int,len:Int) :Unit  
start :开始位置
len：从开始位置向后len个长度

```
val x = List(1,2,3,4,5)//x: List[Int] = List(1, 2, 3, 4, 5)
val a = Array(10,11,12,13,14,15)//a: Array[Int] = Array(10, 11, 12, 13, 14, 15)
x.copyToArray(a,4,3)//
a//res49: Array[Int] = Array(10, 11, 12, 13, 1, 2)

```
列表去重  
def distinct:List[A]
```
val x = List(1,2,3,4,5,2,4)
x.distinct
```
丢弃前n个元素，返回新列表  
def drop(n:Int) :List[A]
```
val x = List(1,2,3,4,5,6)
x.drop(4)
```
丢弃最后n个元素，并返回新列表  
def dropRight(n :Int) : List[A]
```
val x = List(1,2,3,4,5,6)
x.dropRight(4)
```
从左向右丢弃元素，直到条件p不成立  
def dropWhile(p :(A)=>Boolean) :List[A]
```
val x = List(1,2,3,4,5,6,7,8,9)
x.dropWhile(n=>n<4)

```
返回所有的元素，除了第一个  
def init :List[A]
```
val x = List(1,2,3,4,5,6,7,8,9)
x.init
```