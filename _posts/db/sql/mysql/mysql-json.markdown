---
layout: post
title:  "Mysql处理json数据"
date:   2017-08-23 13:21:30
categories: db
tags: sql
---

### 建表
```sql
mysql> CREATE TABLE t1 (jdoc JSON);
```

### 插入
```sql
mysql> INSERT INTO t1 VALUES('{"key1": "value1", "key2": "value2"}');
```

### 修改


### 查询

### 搜索

### 参考
+ [The JSON Data Type](https://dev.mysql.com/doc/refman/5.7/en/json.html)