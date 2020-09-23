---
layout: post
title:  "Oracle创建用户"
date:   2020-01-01 00:00:00
categories: oracle user
---

### 创建用户
```
create user test identified by test_password default tablespace test_space;
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
-- 获取当前用户
SELECT T.* FROM USER_USERS T;
-- 所有用户
SELECT T.* FROM DBA_USERS T;
```

### 添加权限
```
```

### 删除权限
```
```

### 参考
+ [Database SQL Reference](https://docs.oracle.com/cd/B19306_01/server.102/b14200/statements_8003.htm)