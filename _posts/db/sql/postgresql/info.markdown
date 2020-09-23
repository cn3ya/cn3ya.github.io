---
layout: post
title:  "PgSQL查看基本信息"
date:   2017-08-23 13:21:30
categories: db
tags: sql
---

### 查看版本
```sql
select version();
```

### 查看配置信息
```sql
select name, setting from pg_settings;
```

### 参考
+ [JSON Types](https://www.postgresql.org/docs/10/datatype-json.html)
+ [JSON Functions and Operators](https://www.postgresql.org/docs/9.5/functions-json.html)
