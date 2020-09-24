---
layout: post
title:  "[Oracle] 优化器模式"
date:   2020-01-01 00:00:00
categories: oracle user
---

### 优化器模式
Oracle 在执行SQL语句时，有两种优化方法：即基于规则的RBO和基于代价的CBO。 <br/>
在SQL执教的时候，到底采用何种优化方法，就由参数optimizer_mode决定。<br/>
优化器模式影响SQL执行计划中的Cost值。<br/>
查看当前优化器模式
```sql
SELECT * FROM V$PARAMETER WHERE NAME = 'optimizer_mode';
```

### 模式类型
| 模式         | 描述                                                               |
|--------------|--------------------------------------------------------------------|
| ALL_ROWS     | 全部采用基于成本的优化方法CBO                                      |
| FIRST_ROWS_n | 基于成本的优化方法CBO，并以最快的速度，返回前N行记录               |
| FIRST_ROWS   | 使用成本和试探法相结合的方法，查找一种可以最快返回前面少数行的方法 |

### 相关Hint
```sql
/*+ ALL_ROWS */
/*+ FIRST_ROWS */
/*+ FIRST_ROWS (10) */
```

### 修改优化器模式
```sql
-- session
ALTER SESSION SET OPTIMIZER_MODE = FIRST_ROWS;
-- system
ALTER SYSTEM SET OPTIMIZER_MODE = FIRST_ROWS SCOPE=SPFILE;
```

### 参考
+ [Performance Tuning Basics 9 : Optimizer Mode](http://expertoracle.com/2017/11/25/db-tuning-basics-6-optimizier-mode/)
+ [Database Reference](https://docs.oracle.com/en/database/oracle/oracle-database/19/refrn/OPTIMIZER_MODE.html)