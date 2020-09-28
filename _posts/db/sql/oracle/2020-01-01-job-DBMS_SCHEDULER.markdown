---
layout: post
title:  "[Oracle] 定时任务DBMS_SCHEDULER"
date:   2020-01-01 00:00:00
categories: oracle
---

### 创建job_class
```sql
BEGIN
  SYS.DBMS_SCHEDULER.CREATE_JOB_CLASS(JOB_CLASS_NAME          => 'SYS.DEMO_JOB_CLASS',
                                      RESOURCE_CONSUMER_GROUP => 'DEFAULT_CONSUMER_GROUP',
                                      SERVICE                 => '',
                                      LOGGING_LEVEL           => SYS.DBMS_SCHEDULER.LOGGING_RUNS,
                                      LOG_HISTORY             => 14,
                                      COMMENTS                => '定时任务');
END;
```

### 创建定时任务
```sql
BEGIN
  SYS.DBMS_SCHEDULER.CREATE_JOB(JOB_NAME            => 'TEST.TEST',
                                JOB_TYPE            => 'PLSQL_BLOCK',
                                JOB_ACTION          => 'SYSDATE',
                                START_DATE          => TO_DATE('28-09-2020 00:00:00', 'DD-MM-YYYY HH24:MI:SS'),
                                REPEAT_INTERVAL     => 'FREQ=MINUTELY;INTERVAL=1',
                                END_DATE            => TO_DATE(NULL),
                                JOB_CLASS           => 'DEMO_JOB_CLASS',
                                ENABLED             => TRUE,
                                AUTO_DROP           => FALSE,
                                COMMENTS            => '测试任务');
END;
```

### 修改定时任务
```sql
```

### 删除定时任务
```sql
```

### 停用和启用定时任务
```sql
```

### 修改下次执行时间
```sql
```

### 测试执行
```sql
```

### 参考
+ [PL/SQL Packages and Types Reference](https://docs.oracle.com/en/database/oracle/oracle-database/19/arpls/DBMS_SCHEDULER.html)