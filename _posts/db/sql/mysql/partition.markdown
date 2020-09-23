---
layout: post
title:  "MySql分区表"
date:   2017-08-23 13:21:30
categories: db
tags: sql
---

### 创建分区表
```
create table `test_table`
(
    `id`        char(36) not null,
    `create_tm` datetime default current_timestamp,
    `modify_tm` datetime default current_timestamp on update current_timestamp,
    primary key (`id`, `create_tm`)
)
    partition by range ( to_days(create_tm) ) (
        partition p202005 values less than ( to_days('2020-06-01 00:00:00') ),
        partition p202006 values less than ( to_days('2020-07-01 00:00:00') ),
        partition p202007 values less than ( to_days('2020-08-01 00:00:00') ),
        partition p202008 values less than ( to_days('2020-09-01 00:00:00') ),
        partition pmax values less than (maxvalue)
    );
```

### 添删除分区
```
ALTER TABLE test_table DROP PARTITION pmax;
alter table test_table add partition(
    partition p202009 VALUES LESS THAN ( TO_DAYS('2020-10-01 00:00:00') ),
    PARTITION pmax VALUES LESS THAN (MAXVALUE)
);
```