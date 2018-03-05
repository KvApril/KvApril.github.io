---
layout: post
title: "Mysql_Table 'performance_schema.session_variables' doesn't exist"
date: 2018-03-03
description: "Mysql_Table 'performance_schema.session_variables' doesn't exist"
tag: Mysql
--- 

### 问题提示
```
Table 'performance_schema.session_variables' doesn't exist
```

### 更新
```
mysql_upgrade -u root -p --force
```

 
重启
```
sudo /etc/init.d/mysql stop
sudo /etc/init.d/mysql start

```
