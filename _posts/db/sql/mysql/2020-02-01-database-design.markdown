---
layout: post
title:  "[MySQL] 数据库设计"
date: 2020-02-01 00:00:00
categories: db
tags: sql
---

### 主键

自增
迁移时,关联关系维护困难

非自增
插入时,性能变低

结合唯一索引,
主键用来插入, 唯一索引用来关联关系
INSERT IGNORE INTO,
REPLACE INTO,
INSERT INTO ON DUPLICATE KEY UPDATE

```sql
CREATE TABLE `NewTable` (
`index`  bigint UNSIGNED NOT NULL AUTO_INCREMENT ,
`id`  char(36) NOT NULL DEFAULT ''
);
```

### 软删除
deleted
自动归档
