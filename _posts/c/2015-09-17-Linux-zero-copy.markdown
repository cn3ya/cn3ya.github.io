---
layout: post
title:  "[C/C++] linux的zero_copy"
date: 2019-11-01 00:00:00
categories: C++
---

### 实现方式
```
1.直接 I/O
2.mmap
3.sendfile
4.splice
```

### 直接I/O
<linux/iobuf.h>. This file defines struct kiobuf

### mmap

### sendfile

### splice

### 参考
1. [Zero Copy](https://www.linuxjournal.com/article/6345)
2. [Efficient data transfer through zero copy](https://developer.ibm.com/articles/j-zerocopy/)
3. [Chapter 13 mmap and DMA](https://www.xml.com/ldd/chapter/book/ch13.html)
4. [Direct IO](https://tldp.org/HOWTO/SCSI-Generic-HOWTO/dio.html)
5. [splice(2)](https://man7.org/linux/man-pages/man2/splice.2.html)
