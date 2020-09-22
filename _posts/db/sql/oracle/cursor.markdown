---
layout: post
title:  "Oracle游标"
date:   2016-10-11 13:21:30
categories: oracle
---

### parent cursor和child cursor
v$sqlarea中的每一行代表了一个parent cursor，根据address表示了其内存地址。
v$sql中的每一行表示了一个child cursor，根据hash value和address与parent cursor 关联。child cursor有自己的address，即V$SQL.CHILD_ADDRESS。

```
SELECT T.MODULE, T.ACTION, T.VERSION_COUNT, T.*
FROM V$SQLAREA T,
     USER_USERS U
WHERE (T.PARSING_USER_ID = U.USER_ID)
AND
(T.MODULE = 'JDBC Thin Client');
```

```
SELECT T.CHILD_NUMBER, T.LAST_ACTIVE_TIME, T.*
FROM V$SQL T
WHERE T.SQL_ID='1nqd0y53h01v2';
```

### 查看绑定数据
```
SELECT T.INST_ID, T.SQL_ID, T.CHILD_NUMBER, T.POSITION, T.NAME, T.VALUE_STRING
FROM GV$SQL_BIND_CAPTURE T
WHERE T.SQL_ID = 'bqfx5q2jas08u'
  AND T.CHILD_NUMBER = 57
  AND T.INST_ID = 1
ORDER BY T.POSITION;
```

### 查看Child cursor执行计划


### 参考
+ [Performance Tuning Basics 3 : Parent and Child Cursors](http://expertoracle.com/2017/11/17/db-tuning-basics-3-parent-and-child-cursors/)