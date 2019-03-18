---
layout: post
title:  "IO复用"
date:   2016-10-11 13:21:30
categories: C++
---

### 对比

|        | scale | usage      | working way       | complexity |
|:-------|:------|:-----------|:------------------|:-----------|
| select | no      | pass array(读、写、异常分开) | polling all array | O(n)       |
| poll   | no      | pass array(读、写、异常相同) | polling all array | O(n)       |
| epoll  | yes      | register   | report when query | O(n)       |
