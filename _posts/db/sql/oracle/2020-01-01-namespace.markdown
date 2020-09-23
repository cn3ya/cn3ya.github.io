---
layout: post
title:  "Oracle性能调优工具Toad"
date:   2016-10-11 13:21:30
categories: oracle
---

### 查看数据库版本
```
SELECT * FROM V$VERSION;
```

### 查看字符集
```
-- 服务器
SELECT USERENV('LANGUAGE') FROM DUAL;
-- 客户端
SELECT * FROM V$NLS_PARAMETERS;
```

### 

### 参考
+ [Database Reference](https://docs.oracle.com/database/121/REFRN/toc.htm)