---
layout: post
title:  "Mysql索引类型Btree和Hash"
date:   2017-08-23 13:21:30
categories: db
tags: sql
---

### 背景
在写业务代码时,不想使用过多的try...catch方式处理处理很多系统或依赖的exception

### 默认索引类型
下表第一种索引类型为该引擎的默认索引类型

| Storage Engine | Permissible Index Types |
|:---------------|:------------------------|
| InnoDB         | BTREE                   |
| MyISAM         | BTREE                   |
| MEMORY/HEAP    | HASH, BTREE             |
| NDB            | HASH, BTREE             |

### 索引长度
1. innodb_large_prefix配置项关闭(767byte), 打开(3072byte)

### 参考
+ [8.3.8 Comparison of B-Tree and Hash Indexes](https://dev.mysql.com/doc/refman/5.7/en/index-btree-hash.html)
+ [Table 13.1 Index Types Per Storage Engine](https://dev.mysql.com/doc/refman/5.7/en/create-index.html#create-index-storage-engine-index-types)
+ [Limits on InnoDB Tables](https://dev.mysql.com/doc/refman/5.6/en/innodb-restrictions.html)
