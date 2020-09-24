---
layout: post
title:  "[Oracle] Library Cache"
date:   2020-01-01 00:00:00
categories: oracle
---

### 查看Library Cache
LIBRARY CACHE的对象可以在V$DB_OBJECT_CACHE中找到
```sql
SELECT * FROM V$DB_OBJECT_CACHE;
```

### 查看命中率
```
SELECT SUM(pins)                                                "Executions",
       SUM(reloads)                                             "CacheMisses while Executing",
       ROUND((SUM(pins) / (SUM(reloads) + SUM(pins))) * 100, 2) "HitRatio, %"
FROM V$LIBRARYCACHE;
```

### 绑定执行计划


### 参考
+ Oracle Database Reference