---
layout: post
title:  "使用docker搭建PHP开发环境"
date:   2016-10-11 13:21:30
categories: PHP docker
---

### 背景
docker容器技术是当今非常热门的容器技术，他利用linux内核的namespace机制对容器进行隔离，使得各个容器能够相互独立运行，彼此互不干扰。同时相比于虚拟机技术，docker的各个容器之间共享同一份linux内核代码，有着更小的系统开支。

### 开发环境架构设计

#### 1、单容器 or 多容器
对于LNPM开发者来说，一个完整的开发环境，包括linux系统，nginx web服务器，php-fpm守护进程和Mysql数据库。
以往，在使用virtualBox这一类虚拟机技术时，通常的做法是只建一个虚拟机同时运行inux系统，nginx web服务器，php-fpm守护进程和Mysql数据库。但是这与我们实际的生产环境有很大的差别，在高并发的生产环境中，主要以面向服务架构思想为主，系统各个部分被划分为相互独立的低耦合的服务集群，使用负载平衡将短时间的海量请求划分为少量请求分发给集群中的各个节点进行处理。各个服务集群彼此独立运行，互不干扰，任何一个服务宕机并不影响其他服务的运行。
使用一个容器运行一个服务，模拟生产环境中的服务集群，使用多容器更能模拟实际生产环境。现阶段我们需要4个容器。
+ 容器1，nginx web服务
+ 容器2，php-fpm服务
+ 容器3，mysql服务
+ 容器4，redis服务

#### 2、容器与宿主主机的数据交换
docker本身提供文件和文件夹映射的功能,使用命令行参数`-v $(目录):$(容器目录)`或docker-compose.yml配置文件的volumes配置项就可以将宿主机上的文件或文件夹映射到容器中,修改宿主机上的文件容器中文件类容随之改变,灵活运用这一特性可以修改各项服务的配置文件,实时生效代码的修改
```yaml
  volumes:
    - ./www:/usr/share/nginx/html
    - ./conf/default.conf:/etc/nginx/conf.d/default.conf
```
#### 3、容器之间通行
docker命令行工具提供参数`--link`用来关联两个容器,docker-compose也提供links配置项关联容器使得容器之间可以彼此访问
```yaml
  links:
    - redis
    - mysql
```
#### 4、端口映射
为了方便使用navicat等GUI工具对mysql或redis进行访问和管理,需要配置端口映射.
```yaml
  ports:
    - "3306:3306"
```
#### 5、最终docker-compose.yml文件
以下是最终docker-compose.yml配置文件使用命令`docker-compose up -d`可以创建一个php开发环境
```yaml
nginx:
  container_name: my_nginx
  image: nginx:alpine
  ports:
    - "8080:80"
  volumes:
    - ./www:/usr/share/nginx/html
    - ./conf/default.conf:/etc/nginx/conf.d/default.conf
  links:
    - php-fpm

php-fpm:
  container_name: my_php-fpm
  image: cn3ya/docker-php
  expose:
    - "9000"
  volumes:
    - ./www:/var/www/html
  links:
    - redis
    - mysql

redis:
  container_name: my_redis
  image: redis:alpine
  command: redis-server --requirepass php
  expose:
    - "6379"
  ports:
    - "6379:6379"

mysql:
  container_name: my_mysql
  image: mysql
  ports:
    - "3306:3306"
  environment:
    - MYSQL_ROOT_PASSWORD=php
    - MYSQL_DATABASE=php
    - MYSQL_USER=php
    - MYSQL_PASSWORD=php
```
