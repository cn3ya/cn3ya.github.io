---
layout: post
title:  "[Oracle] Shared Pool"
date:   2020-01-01 00:00:00
categories: oracle
---

### 清除缓存
```sql
select ADDRESS, HASH_VALUE from V$SQLAREA where SQL_ID like '7yc%';
-- ADDRESS          HASH_VALUE
-- 000000085FD77CF0  808321886
exec DBMS_SHARED_POOL.PURGE ('000000085FD77CF0, 808321886', 'C');
-- ‘C’ (for cursor) or ‘S’ (for SQL)
```

### 参考
+ [PL/SQL Packages and Types Reference](https://docs.oracle.com/en/database/oracle/oracle-database/19/arpls/DBMS_SHARED_POOL.html)