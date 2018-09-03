---
layout: post
title:  "使用Grafana,InfluxDB和Telegraf打造监控平台"
date:   2015-09-22 09:41:22
categories: Granfana InfluxDB Telegraf
---

### 背景
在生产环境中,通过人力无法实现7x24的对服务器的监控

### 安装
#### 环境
```shell
#docker --version
Docker version 18.04.0-ce, build 3d479c0
```
#### 拉取镜像
```shell
docker pull grafana/grafana influxdb telegraf
```
#### 编写docker-compose.yml文件
```yml

```
#### 编写telegraf配置文件
验证配置
```shell
telegraf --test --config /etc/telegraf/telegraf.d/node.conf

influx
show databases
show measurements
select * from mem
```
#### 配置grafana读取influxdb
看板参数设置
show tag values from cpu with key = host

### 需求

####1、监控服务器性能指标

####2、监控服务健康状态

####3、异常提醒
