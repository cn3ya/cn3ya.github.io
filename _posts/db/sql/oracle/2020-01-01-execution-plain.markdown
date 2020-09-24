---
layout: post
title:  "[Oracle] 执行计划"
date:   2020-01-01 00:00:00
categories: oracle
---

### 查看执行计划
每种类型的dml语句都需要如下阶段：
1. Create a Cursor         创建游标
2. Parse the Statement     解析语句
3. Bind Any Variables      绑定变量
4. Run the Statement       运行语句
5. Close the Cursor        关闭游标

查看执行计划
```sql
EXPLAIN PLAN FOR
      SELECT * FROM SCOTT.EMP;

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY);
```

### 查看历史执行计划
```sql
SELECT t1.SQL_TEXT,
       t1.SQL_FULLTEXT,
       t2.ID,
       t2.OPERATION,
       t2.OPTIONS,
       t2.OBJECT_OWNER,
       t2.OBJECT_NAME,
       t2.COST,
       t2.CARDINALITY,
       t2.BYTES
FROM V$SQLAREA t1,
     V$SQL_PLAN t2
WHERE t1.ADDRESS = t2.ADDRESS
  AND t1.HASH_VALUE = t2.HASH_VALUE
  AND t1.SQL_ID='b9t70mw0m2wqw';
```

### 绑定执行计划
```sql

```

### 查看统计信息
```sql
-- 表
SELECT TABLE_NAME, BLOCKS, NUM_ROWS, LAST_ANALYZED
FROM USER_TAB_STATISTICS T
ORDER BY LAST_ANALYZED DESC;
-- 列
SELECT T.TABLE_NAME,
       T.COLUMN_NAME,
       T.NUM_DISTINCT,
       T.LOW_VALUE,
       T.HIGH_VALUE,
       LAST_ANALYZED
  FROM USER_TAB_COL_STATISTICS T;
```

### 参考
+ Oracle Database Reference