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
view    AllView         included        1.3.6.1
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
snmpwalk -v 2c -c config-user 127.0.0.1 1.3.6.1.2.1.1
snmpwalk -v 2c -c config-user -On 127.0.0.1 1.3.6.1.2.1.1
```

### 需求

#### 1、通用性能指标
参考
```
http://www.oidview.com/mibs/0/HOST-RESOURCES-MIB.html
https://www.alvestrand.no/objectid/1.3.6.1.2.1.1.3.html
https://www.centos.org/forums/viewtopic.php?t=49064
```
不同设备和操作系统有可能OID不同.

||指标|OID|
|-|-|-|
|1|主机名|1.3.6.1.2.1.1.5.0|
|2|运行时间|1.3.6.1.2.1.25.1.1|
|2|服务器时间|1.3.6.1.2.1.25.1.2|
|2|当前登录用户数量|1.3.6.1.2.1.25.1.5|
|4|当前进程数量|1.3.6.1.2.1.25.1.6|
|4|最大进程数量|1.3.6.1.2.1.25.1.7|
|3|CPU负载|1.3.6.1.4.1.2021.10.1.3|
|5|内存IO|1.3.6.1.4.1.2021.4.11|
|6|磁盘IO|1.3.6.1.2.1.25.2.3.1|
|7|网络IO|1.3.6.1.2.1.2.2.1.2|

#### 2、特定指标
