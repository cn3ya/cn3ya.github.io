---
layout: post
title:  "[Oracle] Group类型"
date:   2020-01-01 00:00:00
categories: oracle
---

### 总览
join 类型<br/>
Both the RBO and CBO support these three join types: nested loop, merge join and hash join.

driving table, outter table
inner table


#参考https://logicalread.com/oracle-explain-plans-driving-tables-and-table-joins-h01/#.X3GQsGgzbPo
### nested loop
The driving table is read once and for each row in the driving table, the inner table is processed once.  The smaller the inner result set, the faster the Nested Loop will perform.
二重循环，遍历内部表每条记录，循环比较外部表的所有记录，适合内部表比较小

### merge join / sort join
The driving table is the first one, but in this case, it doesn’t really matter which table is first and second.  Both tables are sorted.  Then the returning rows are merged together and passed to the next step on the explain plan tree.
内部表和外部表都先排序，后连接，适合内部表和外部表都较大，大小相近

### hash join
The driving table should be the smaller.  Oracle loads the driving table into a hash table first, then looks up each row in this hash table in the inner table.  So, the smaller table should be first, or the driving table.
外部表现计算hash，遍历内部表每条记录，按hash查找外部表记录，适合外部表比较小，如配置表


### 参考
+ [How to Read an Execution Plan](https://blogs.oracle.com/oraclemagazine/how-to-read-an-execution-plan)