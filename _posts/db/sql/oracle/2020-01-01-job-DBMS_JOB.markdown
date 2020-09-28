---
layout: post
title:  "[Oracle] 定时任务DBMS_JOB"
date:   2020-01-01 00:00:00
categories: oracle
---

### 查看定时任务
```sql
SELECT * FROM USER_JOBS;
SELECT * FROM DBA_JOBS;
SELECT * FROM DBA_JOBS T WHERE T.WHAT LIKE '%TEST%';
```

### 创建定时任务
```sql
DECLARE JOBNUMBER NUMBER;
BEGIN
    SYS.DBMS_JOB.SUBMIT(
        JOB => JOBNUMBER,
        WHAT => 'sysdate',
        NEXT_DATE => SYSDATE + 1 / 24,
        INTERVAL => 'SYSDATE + 1 / 24'
    );
    COMMIT;
END;
```

### 修改定时任务
```sql
BEGIN
    DBMS_JOB.WHAT(1, SYSDATE); -- job_id, what
    DBMS_JOB.INTERVAL(1,TRUNC(SYSDATE) + 1); -- job_id, interval
    COMMIT;
END;
```

### 删除定时任务
```sql
BEGIN
    DBMS_JOB.REMOVE(483); -- job_id
    COMMIT;
END;
```

### 停用和启用定时任务
```sql
BEGIN
    DBMS_JOB.BROKEN(687,FLASE); -- 停用
    DBMS_JOB.BROKEN(687,TRUE,SYSDATE); -- 启用
    COMMIT;
END;
```

### 修改下次执行时间
```sql
BEGIN
    DBMS_JOB.NEXT_DATE(483, TO_DATE('2019-11-18 16:53:00','YYYY-MM-DD HH24:MI:SS')); -- job_id, next_date
    COMMIT;
END;
```

### 测试执行
```sql
BEGIN
    DBMS_JOB.RUN(1); -- job_id
    COMMIT;
END;
```

### 时间语法
```sql
-- 每分钟
sysdate + 1/24/60
-- 每小时
sysdate + 1/24
-- 每天
sysdate + 1
-- 每天 6:00
trunc(sysdate + 1) + 6/24
-- 每周
sysdate + 7
-- 每月1号 6:00
trunc(last_day(sysdate) + 1) + 6/24
```

### 参考
+ [PL/SQL Packages and Types Reference](https://docs.oracle.com/en/database/oracle/oracle-database/19/arpls/DBMS_JOB.html)