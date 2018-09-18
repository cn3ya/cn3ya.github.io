---
layout: post
title:  "Mysql分区表"
date:   2015-09-22 09:41:22
categories: mysql increment_backup
---

### 背景
备份生产环境的数据库,经常使用增量备份

### 优点
1、冷热分离：表非常大且只在表的最后部分有热点数据，冷数据根据分区规则自动归档。

2、定期淘汰历史数据：按时间写入，历史数据可淘汰，可快速删除，空间可快速回收。

3、优化查询：在where字句中包含分区列时，分区可以大大提高查询效率，减少缓存开销、减少IO开销。

4、统计性能提升：在涉及sum()和count()这类聚合函数的查询时，可以在每个分区上面并行处理，最终只需要汇总所有分区得到的结果。

### 分区规则

| 类型          |
|:-------------|
| RANGE        |
| LIST         |
| HASH         |
| KEY          |
| SUBPARTITION |

### 性能对比


### 参考
+ [MySQL·最佳实践·分区表基本类型](http://mysql.taobao.org/monthly/2017/11/09/)
+ [Chapter 22 Partitioning](https://dev.mysql.com/doc/refman/5.7/en/partitioning.html)
