---
layout: post
title:  "Linux内核调试"
date:   2016-10-11 13:21:30
categories: Ruby
---

### 编译busybox
```bash
#安装glibc静态库
yum install -y glibc-static
make
make install
```

### 创建initramfs
创建目录结构
```
mkdir initramfs
mkdir -p bin sbin etc proc sys usr/bin usr/sbin
cp -a ../busybox/_install/* .
```
创建`/init`脚本
```bash
#!/bin/sh
mount -t proc none /proc
mount -t sysfs none /sys
exec /bin/sh
```
打包成initramfs文件
```
find . -print0 | cpio --null -ov --format=newc \
  | gzip -9 > $BUILDS/initramfs.cpio.gz
```

### 编译kernel

### 启动qemu
```
qemu-system-x86_64 -kernel bzImage -initrd initramfs.cpio.gz
```

### 参考
+ [Build and run minimal Linux / Busybox systems in Qemu](https://gist.github.com/chrisdone/02e165a0004be33734ac2334f215380e)