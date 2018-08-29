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
snmpwalk -v 2c -c config-user localhost     1.3.6.1.2.1.1
snmpwalk -v 2c -c config-user -On localhost 1.3.6.1.2.1.1
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
|3|服务器时间|1.3.6.1.2.1.25.1.2|
|4|当前登录用户数量|1.3.6.1.2.1.25.1.5|
|5|当前进程数量|1.3.6.1.2.1.25.1.6|
|6|最大进程数量|1.3.6.1.2.1.25.1.7|
|7|CPU负载|1.3.6.1.4.1.2021.10|
|8|内存IO|1.3.6.1.4.1.2021.4|
|9|磁盘信息|1.3.6.1.2.1.25.2.3.1|
|10|磁盘IO|1.3.6.1.4.1.2021.13|
|11|网络IO|1.3.6.1.2.1.2.2.1.2|
修改配置文件
```shell
#       sec.name        source          community
com2sec ConfigUser      default         config-user
#                       sec.model       sec.name
group   AllGroup        v2c             ConfigUser
#                       incl/excl       subtree
#hostname
view    AllView         included        1.3.6.1.2.1.1.5.0
#network_io
view    AllView         included        1.3.6.1.2.1.2.2.1
#uptime
view    AllView         included        1.3.6.1.2.1.25.1.1
#date
view    AllView         included        1.3.6.1.2.1.25.1.2
#login_user
view    AllView         included        1.3.6.1.2.1.25.1.5
#process_num
view    AllView         included        1.3.6.1.2.1.25.1.6
#max_process_num
view    AllView         included        1.3.6.1.2.1.25.1.7
#disk_info
view    AllView         included        1.3.6.1.2.1.25.2.3.1
#mem_io
view    AllView         included        1.3.6.1.4.1.2021.4
#cpu_load
view    AllView         included        1.3.6.1.4.1.2021.10
#disk_io
view    AllView         included        1.3.6.1.4.1.2021.13
#                       context model   level   prefix  read            write   notify
access  AllGroup        ""      any     noauth  exact   AllView         none    none
```
#### 2、特定指标
参考
```
https://www.juniper.net/documentation/en_US/junos/topics/example/junos-script-automation-snmp-script-example.html
```
当监控参数没有通用OID时,需要我们自己编写脚本来获取数据
