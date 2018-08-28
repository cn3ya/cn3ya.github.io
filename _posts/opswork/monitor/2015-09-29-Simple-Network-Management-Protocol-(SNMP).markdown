---
layout: post
title:  "使用SNMP监控服务器性能"
date:   2015-09-22 09:41:22
categories: CouldFlare CDN DNS
---

### 背景
对服务器数据的收集,是实现服务器监控的首要任务

### 环境
```shell
#cat /etc/redhat-release
CentOS Linux release 7.4.1708 (Core)
```
### 安装
下载依赖文件
```shell
yum -y install net-snmp net-snmp-utils
```
修改配置文件`/etc/snmp/snmpd.conf`
```shell
#       sec.name        source          community
com2sec ConfigUser      default         config-user
#                       sec.model       sec.name
group   AllGroup        v2c             ConfigUser
#                       incl/excl       subtree
view    AllView         included        1.3.6.1.2.1.1
#                       context model   level   prefix  read            write   notify
access  AllGroup        ""      any     noauth  exact   AllView         none    none
```
启动服务
```shell
systemctl start snmpd
systemctl enable snmpd
```
验证安装
```shell
snmpwalk -v 2c -c config-user -O 127.0.0.1
snmpwalk -v 2c -c config-user -On 127.0.0.1
```

### 需求

#### 1、通用性能指标
参考`https://www.alvestrand.no/objectid/1.3.6.1.2.1.1.3.html`,不同设备和操作系统有可能OID不同.

||指标|OID|
|-|-|-|
|1|主机名| .1.3.6.1.2.1.1.5.0 |
|2|运行时间| .1.3.6.1.2.1.1.3.0 |
|3|CPU负载||
|4|进程数量||
|5|内存IO||
|6|磁盘IO||
|7|网络IO||

#### 2、特定指标
