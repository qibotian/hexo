---
title: Redis数据类型
date: 2020-04-28
categories: ['Redis']
tags: [Redis','缓存']
comments: true
id: redisDataType
---



<!--more-->

Redis 有5中基本的数据类型

# String

格式： > set key value  
最基本的数据格式，一个键最大可以保存512M内容

# Hash

格式: > set name k1 value1 key2 value2

# List

格式: > lpush/rpush name value

# Set

格式：>sadd name value

# ZSet

格式：>zadd name value
