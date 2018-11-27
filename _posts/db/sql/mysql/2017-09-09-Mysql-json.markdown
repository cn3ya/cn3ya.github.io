---
layout: post
title:  "Mysql处理json数据"
date:   2017-08-23 13:21:30
categories: db
tags: sql
---

### 插入
```sql
mysql> CREATE TABLE t1 (jdoc JSON);
Query OK, 0 rows affected (0.20 sec)

mysql> INSERT INTO t1 VALUES('{"key1": "value1", "key2": "value2"}');
Query OK, 1 row affected (0.01 sec)
```

### 修改


### 查询

### 参考
+ [The JSON Data Type](https://dev.mysql.com/doc/refman/5.7/en/json.html)