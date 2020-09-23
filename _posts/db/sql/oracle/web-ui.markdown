---
layout: post
title:  "Oracle网页管理"
date:   2020-01-01 00:00:00
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
+ Oracle Database Reference