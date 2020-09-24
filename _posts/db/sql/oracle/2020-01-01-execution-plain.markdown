---
layout: post
title:  "[Oracle] 执行计划"
date:   2020-01-01 00:00:00
categories: oracle
---

### 查看执行计划
每种类型的dml语句都需要如下阶段：
```
Create a Cursor         创建游标
Parse the Statement     解析语句
Bind Any Variables      绑定变量
Run the Statement       运行语句
Close the Cursor        关闭游标
```
查看执行计划
```
EXPLAIN PLAN FOR
      SELECT * FROM SCOTT.EMP;

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY);
```

### 查看历史执行计划
```

```

### 绑定执行计划
```
```

### 参考
+ Oracle Database Reference