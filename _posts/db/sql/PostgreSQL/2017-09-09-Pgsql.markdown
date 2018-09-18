---
layout: post
title:  "PgSQL数据库"
date:   2017-08-23 13:21:30
categories: db
tags: sql
---

### 术语

| item     | 描述   |
|:---------|:------|
| database | 数据库 |
| schema   | 表空间 |
| table    | 数据表 |

### 基本操作
#### 使用psql
```
psql --username=postgres
```
S标识是否显示系统内置信息

| 命令                           | 说明            |
|:------------------------------|:---------------|
| \\?                           | 查看所有支持的命令 |
| \\l                           | 列出所有数据库    |
| \\c dbName                    | 切换数据库       |
| \\dn[S]                       | 列出表空间       |
| show search_path;             | 查看表空间搜索路径 |
| SET search_path TO schemaName | 设置表空间搜索路径 |
| \\dt[S]                       | 列出数据表       |
| \\q                           | 退出            |
### 默认表空间(pg_catalog)
#### 查看所有数据表信息
```sql
SELECT * FROM pg_catalog.pg_tables;
```

### 环境变量

|           |               |
|:----------|:--------------|
| show all; | 查看所有环境变量 |
| $user     | 当前登录用户    |


### 参考
+ [PostgreSQL百亿数据 秒级响应 正则及模糊查询](https://github.com/digoal/blog/blob/master/201603/20160302_01.md)
