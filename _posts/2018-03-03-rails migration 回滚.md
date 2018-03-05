---
layout: post
title: "rails_migration 回滚"
date: 2018-03-03
description: "rails_migration 回滚"
tag: Rails
--- 

如果刚修改的migration文件有问题，可以对刚才的行为进行回退，重新编辑后再迁移  

### 回退一步
```
rake db:rollback STEP=1
```
### 回退多步

```
rake db:rollback STEP=5 #这会使近五次的迁移都被回滚
```

### 回滚特定版本的迁移文件

```
rake db:migrate:down VERSION=20100905201547
```

### 列举所有的迁移版本

```
rake db:migrate:status

database: xxxxxxxxxx
 Status   Migration ID    Migration Name
--------------------------------------------------
   up     20170314070801  Create undergraduate students
   up     20170314070802  Create undergraduate classes
   up     20170314070803  Create undergraduate majors
   up     20170314070804  Create departments
   up     20170314070805  Create access points
   up     20170314070806  Create employees
   up     20170314070807  Create user macs
   up     20170315070903  Create users
..........
..........
```
