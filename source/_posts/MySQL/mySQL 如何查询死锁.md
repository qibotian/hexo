---
title: MySQL 如何查询死锁
date: 2019-08-12
categories: ['MySQL']
tags: ['MySQL','死锁',]
comments: true
id: mysqlDeadLock
---

如何查询MYSQL死锁，及排查问题的方法

<!--more-->

## 查询当前所有运行的线程
  ```
  select id, db, user, host, command, time, state, info
  FROM information_schema.processlist WHERE db = 'some_db' ORDER BY id ASC;
  ```
## 查看当前使用的表
  ```
    SHOW OPEN TABLES WHERE In_use > 0;
  ```

## 查看当前所有事务
  ```
    SELECT * FROM INFORMATION_SCHEMA.INNODB_TRX;
  ```

## 查看当前锁定事务

```
  SELECT * FROM INFORMATION_SCHEMA.INNODB_LOCKS;
```

## 查看当前等待锁的事务
```
  SELECT * FROM INFORMATION_SCHEMA.INNODB_LOCK_WAITS;

```

## 综合SQL

```
SELECT
t1.requesting_trx_id AS '请求事务ID',
t1.requested_lock_id AS '请求锁Id',
t1.blocking_trx_id AS '阻塞事务Id',
t1.blocking_lock_id '阻塞锁id',
'|| 阻塞事务信息 ||',
t2.lock_mode AS '锁模型',
t2.lock_type AS '锁类型',
lock_table '锁表',
lock_index '锁索引',
lock_space '锁space',
lock_space '锁页面',
lock_rec 'lock_rec',
lock_data '锁数据',
t3.trx_state AS '事务状态',
t3.trx_started '事务开始时间',
t3.trx_requested_lock_id '正在等待的锁的ID',
t3.trx_wait_started '交易开始等待锁定的时间',
t3.trx_weight '事务的权重',
t3.trx_mysql_thread_id '线程Id',
t3.trx_query '执行语句',
t4.COMMAND AS '线程命令',
t4.time '线程等待时间',
t4.state '线程状态',
t4.INFO '线程信息'
FROM
INFORMATION_SCHEMA.INNODB_LOCK_WAITS AS t1
LEFT JOIN INFORMATION_SCHEMA.INNODB_LOCKS AS t2 ON t1.blocking_lock_id = t2.lock_id
LEFT JOIN INFORMATION_SCHEMA.INNODB_TRX AS t3 ON t1.blocking_trx_id = t3.trx_id
LEFT JOIN information_schema. PROCESSLIST AS t4 ON t3.trx_mysql_thread_id = t4.ID
UNION
SELECT
  t1.requesting_trx_id AS '请求事务ID',
  t1.requested_lock_id AS '请求锁Id',
  t1.blocking_trx_id AS '阻塞事务Id',
  t1.blocking_lock_id '阻塞锁id',
  '|| 等待事务信息 ||',
  t2.lock_mode AS '锁模型',
  t2.lock_type AS '锁类型',
  t2.lock_table '锁表',
  t2.lock_index '锁索引',
  t2.lock_space '锁space',
  t2.lock_space '锁页面',
  t2.lock_rec 'lock_rec',
  t2.lock_data '锁数据',
  t3.trx_state AS '事务状态',
  t3.trx_started '事务开始时间',
  t3.trx_requested_lock_id '正在等待的锁的ID',
  t3.trx_wait_started '交易开始等待锁定的时间',
  t3.trx_weight '事务的权重',
  t3.trx_mysql_thread_id '线程Id',
  t3.trx_query '执行语句',
  t4.COMMAND AS '线程命令',
  t4.time '线程等待时间',
  t4.state '线程状态',
  t4.INFO '线程信息'
FROM
  INFORMATION_SCHEMA.INNODB_LOCK_WAITS AS t1
LEFT JOIN INFORMATION_SCHEMA.INNODB_LOCKS AS t2 ON t1.requested_lock_id = t2.lock_id
LEFT JOIN INFORMATION_SCHEMA.INNODB_TRX AS t3 ON t1.requesting_trx_id = t3.trx_id
LEFT JOIN information_schema. PROCESSLIST AS t4 ON t3.trx_mysql_thread_id = t4.ID

```
