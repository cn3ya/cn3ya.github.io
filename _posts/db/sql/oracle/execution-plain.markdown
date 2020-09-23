---
layout: post
title:  "Oracle执行计划"
date:   2016-10-11 13:21:30
categories: oracle
---

### 查看执行计划
每种类型的dml语句都需要如下阶段：

Create a Cursor         创建游标
Parse the Statement     解析语句
Bind Any Variables      绑定变量
Run the Statement       运行语句
Close the Cursor        关闭游标

```
EXPLAIN PLAN FOR
      SELECT * FROM SCOTT.EMP;

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY);
```

### 查看历史执行计划
```

```

### 绑定执行计划


### 参考
+ Oracle Database Reference