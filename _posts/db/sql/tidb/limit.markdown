---
layout: post
title:  "TiDB使用限制"
date:   2016-10-11 13:21:30
categories: tidb
---

### 事务大小限制
```
CREATE TABLESPACE TEST_SPACE
DATAFILE '/ORADATA/ORCL/TEST_SPACE.DBF' SIZE 1000M;
```
使用小事务
大表不能使用INSERT INTO ... SELECT FROM语句
绕过事务限制
set @@session.tidb_batch_insert=1;
### 主键问题

### 分区表

### 增删字段

### 增删字段索引

### limit无序

### 参考
+ Oracle Database Reference