---
layout: post
title:  "[Oracle] 数据字典(元数据)表"
date:   2020-01-01 00:00:00
categories: oracle
---

### 描述
Static Data Dictionary Views
oracle的数据字典表，或数据库元数据表，存储了描述数据库的运行信息，如数据表信息，用户信息，和权限信息等。创建和修改表，修改用户和权限变更将会改变这些信息，

### 命名规则和分类
查看所有可用的数据字典(元数据)表和试图
```
SELECT * FROM DICTIONARY;
```
ALL_*, 当前用户可以访问的所有数据库对象。
USER_*, 当前用户当前数据库的对象。
DBA_*，所有数据库对象。

V$*, 动态性能数据表和试图
GV$*, 全局动态性能数据表和试图，增加INST_ID字段

### 常用表和试图
*_ALL_TABLES,
*_COL_COMMENTS

### 参考
+ Oracle Database Reference
