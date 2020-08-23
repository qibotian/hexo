---
title: linux安装Redis
date: 2020-08-03
categories: ['Redis']
tags: ['Redis']
comments: true
id: installRedisOnLinux
---

linux中安装Redis
<!--more-->


[TOC]

###1 首先查看自己的gcc版本
```bash
gcc --version

#如果输出的7版本以下的话，则编译可能会失败，需要安装更高版本的gcc

$ sudo yum install centos-release-scl
$ sudo yum install devtoolset-7
$ sudo yum install devtoolset-7-gcc
$ scl enable devtoolset-7 bash

#这个时候再输出gcc版本，应该就是7版本了

$ gcc --version
gcc (GCC) 7.2.1 20170829 (Red Hat 7.2.1-1)

# 设置永久生效
$ source /opt/rh/devtoolset-7/enable
# 或者
$ source scl_source enable devtoolset-7

```

###2 下载最新的redis,并进行安装

```bash
#进入到下载目录
$ cd /usr/download

#下载最新的安装包
$ wget http://download.redis.io/redis-stable.tar.gz

#解压
$ tar -xzvf redis-stable.tar.gz

#编译
$ cd redis-stable
$ make

#安装到 /opt/redis下
$ cd src
$ make install PREFIX=/opt/redis

# 将配置文件拷贝到/opt/redis下
$ cp redis.conf /opt/redis

# 将redis设置为开机启动
$ vi /etc/rc.local

##在里面添加内容：
/opt/redis/bin/redis-server /opt/redis/redis.conf

# 开启远程访问
$ vim /opt/redis/redis.conf
## 将文件中 protected-mode改为 no， 注释掉bind 127.0.0.1


#启动redis

$ /opt/redis/bin/redis-server /opt/redis/redis.conf

```

###3. 如何卸载Redis
```bash
$ rm -rf /opt/redis //删除安装目录
$ rm -rf /usr/bin/redis-* //删除所有redis相关命令脚本
$ rm -rf /usr/download/redis-* //删除redis解压文件夹
```
