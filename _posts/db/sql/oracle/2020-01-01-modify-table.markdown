---
layout: post
title:  "[Oracle] 大数据表修改特性"
date:   2020-01-01 00:00:00
categories: oracle
---

### 参考数据量
1. 字段数量: 16
2. 记录数据量: 6000w

### 增删字段
```sql
alter table LINEITEM add test varchar2(36) default '';
comment on column LINEITEM.test
  is '测试';
-- 1s
alter table LINEITEM drop column test;
-- 2:59m
```

### 增删索引
```sql
create index test_idx on LINEITEM (l_orderkey);
-- 8:10m
drop index TEST_IDX;
-- 2s
```

### 是否锁表
```
```

### 参考
+ Oracle Database Reference