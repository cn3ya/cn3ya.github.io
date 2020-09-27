---
layout: post
title:  "[MySQL] 分区表"
date: 2020-02-01 00:00:00
categories: db
tags: sql
---

### 创建分区表
```sql
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
```sql
ALTER TABLE test_table DROP PARTITION pmax;
alter table test_table add partition(
    partition p202009 VALUES LESS THAN ( TO_DAYS('2020-10-01 00:00:00') ),
    PARTITION pmax VALUES LESS THAN (MAXVALUE)
);
```

### 查看分区
```sql
SELECT *
FROM information_schema.PARTITIONS T
WHERE T.TABLE_NAME='test_table';
```


### 查看分区数据
```sql
SELECT * FROM test_table PARTITION (p202005);
```