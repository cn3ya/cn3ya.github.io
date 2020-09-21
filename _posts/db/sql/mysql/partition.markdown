---
layout: post
title:  "MySql分区表"
date:   2017-08-23 13:21:30
categories: db
tags: sql
---

### 创建分区表
```
CREATE TABLE `test_table`
(
  `id`                   char(36)       NOT NULL,
	`create_tm`      datetime       DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`id`,`create_tm`)
)
  PARTITION BY RANGE ( TO_DAYS(create_tm) ) (
  PARTITION p202005 VALUES LESS THAN ( TO_DAYS('2020-06-01 00:00:00') ),
  PARTITION p202006 VALUES LESS THAN ( TO_DAYS('2020-07-01 00:00:00') ),
  PARTITION p202007 VALUES LESS THAN ( TO_DAYS('2020-08-01 00:00:00') ),
  PARTITION p202008 VALUES LESS THAN ( TO_DAYS('2020-09-01 00:00:00') ),
  PARTITION pmax VALUES LESS THAN (MAXVALUE)
);
```

### 添加分区
```
ALTER TABLE test_table DROP PARTITION pmax;
alter table test_table add partition(
    partition p202009 VALUES LESS THAN ( TO_DAYS('2020-10-01 00:00:00') ),
    PARTITION pmax VALUES LESS THAN (MAXVALUE)
);
```