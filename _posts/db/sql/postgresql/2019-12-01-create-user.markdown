---
layout: post
title:  "[PgSQL] 创建用户"
date: 2019-12-01 00:00:00
categories: PostgreSQL PGSQL
---

### 创建用户
```
create user test with password 'test333';
CREATE DATABASE testdb OWNER test;
GRANT ALL PRIVILEGES ON DATABASE testdb TO test;
```

### 删除用户
```
drop user test cascade;
```

### 修改用户
```
create user test identified by test_password default tablespace test_space;
```

### 查看用户
```
select * from pg_user;
```

### 添加权限
```
```

### 删除权限
```
```

### 参考
+ [Database SQL Reference](https://docs.oracle.com/cd/B19306_01/server.102/b14200/statements_8003.htm)