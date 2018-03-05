---
layout: post
title: "Scala_Array"
date: 2018-03-03
description: "Scala_Array"
tag: Scala
--- 
方法:**def addString(b: StringBuilder): StringBuilder**  
return: StringBuilder()
```
val a = Array(1,2,3,4) # a: Array[Int] = Array(1, 2, 3, 4)
val b = new StringBuilder() # b: StringBuilder =
val c = a.addString(b) # c: StringBuilder = 1234



val a = List(1,2,3,4) # List[Int] = List(1, 2, 3, 4)
val b = new StringBuilder("kv") # b: StringBuilder = kv
val c = a.addString(b) # c: StringBuilder = kv1234

```

方法：**def addString(b: StringBuilder, sep: String): StringBuilder**  
seq:分割字符
```
val a = Array(1,2,3,4)# a: Array[Int] = Array(1, 2, 3, 4)
val b = new StringBuidler()# b: StringBuilder =
val c = a.addString(b,"--")# c: StringBuilder = 1--2--3--4

val a = Array(1,2,3,4)# a: Array[Int] = Array(1, 2, 3, 4)
val b = new StringBuilder("kv")# b: StringBuilder = kv
val c = a.addString(b,"--")# c: StringBuilder =kv1--2--3--4

val a = Array(1,2,3,4)# a: Array[Int] = Array(1, 2, 3, 4)
val b = new StringBuilder("kv")# b: StringBuilder = kv
val c = a.addString(b,"**")# c: StringBuilder =kv1**2**3**4

```
方法：**def addString(b: StringBuilder, start: String, sep: String, end: String): StringBuilder**  
start:开始字符  
end:结束字符  
seq:分割字符

```
val a = Array(1,2,3,4)# a: Array[Int] = Array(1, 2, 3, 4)
val b = new StringBuilder() # b: StringBuilder =
val c = a.addString(b,"ss","--","eed")#c: StringBuilder = ss1--2--3--4eed


val a = Array(1,2,3,4)# a: Array[Int] = Array(1, 2, 3, 4)
val b = new StringBuilder("kv") # b: StringBuilder = kv
val c = a.addString(b,"ss","--","eed")#c: StringBuilder = kvss1--2--3--4eed

val a = Array(1,2,3,4)# a: Array[Int] = Array(1, 2, 3, 4)
val b = new StringBuilder("kv") # b: StringBuilder = kv
val c = a.addString(b,"List(",",",")")#c: StringBuilder = kvList(1,2,3,4)

```



