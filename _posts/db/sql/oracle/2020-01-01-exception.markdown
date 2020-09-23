---
layout: post
title:  "Oracle异常处理"
date:   2020-01-01 00:00:00
categories: oracle
---

### 存储过程
```sql
-- 设置模块和动作名
EXEC DBMS_APPLICATION_INFO.SET_MODULE('TEST-MODULE','TEST-ACTION');
-- 设置动作名
EXEC DBMS_APPLICATION_INFO.SET_ACTION('TEST-ACTION');

-- 错误栈
DBMS_UTILITY.format_error_backtrace
DBMS_OUTPUT.put_line (DBMS_UTILITY.format_error_backtrace);

-- 自定义错误
raise_application_error()
```

### 异常处理
```sql
-- proc1
CREATE OR REPLACE PROCEDURE PROC1
AS
    FLAG INT;
    RETRUN_EX EXCEPTION;
    PRAGMA EXCEPTION_INIT (RETRUN_EX, -20001);
BEGIN
    DBMS_OUTPUT.PUT_LINE('Running PROC1');
    FLAG := DBMS_RANDOM.RANDOM;
    IF MOD(FLAG, 2) = 0 THEN
        DBMS_OUTPUT.PUT_LINE('FLAG=' || FLAG);
        RAISE_APPLICATION_ERROR(-20001, 'RETURN');
    ELSE
        DBMS_OUTPUT.PUT_LINE('FLAG=' || FLAG);
        RAISE_APPLICATION_ERROR(-20001, 'RETURN');
    END IF;
EXCEPTION
    WHEN RETRUN_EX
        THEN
            DBMS_OUTPUT.PUT_LINE(REPLACE(DBMS_UTILITY.FORMAT_ERROR_BACKTRACE, 'ORA-06512', 'RETURN'));
    WHEN OTHERS
        THEN
            DBMS_OUTPUT.PUT_LINE(SQLERRM);
END;
-- TEST
CALL proc1();
```

### sql定位


### 参考
+ Oracle Database Reference