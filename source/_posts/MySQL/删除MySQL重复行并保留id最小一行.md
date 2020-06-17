---
title: 删除MySQL重复行并保留id最小一行
date: 2019-05-15
categories: ['MySQL']
tags: ['MySQL']
comments: true
id: delete-repeat-row-without-min-id
---

# 1. 表结构

```sql

DROP TABLE IF EXISTS `dept`;
CREATE TABLE `dept` (
`id` int(11) NOT NULL,
`name` varchar(255) DEFAULT NULL,
PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=gbk;


INSERT INTO `dept` VALUES ('0', '1_组');
INSERT INTO `dept` VALUES ('1', '1_组');
INSERT INTO `dept` VALUES ('2', '1_组');
INSERT INTO `dept` VALUES ('3', '2_组');
INSERT INTO `dept` VALUES ('4', '2_组');
INSERT INTO `dept` VALUES ('5', '3_组');
INSERT INTO `dept` VALUES ('6', '4_组');
INSERT INTO `dept` VALUES ('7', '4_组');

```

# 2. 查询重复行

```sql
SELECT
	*
FROM
	dept AS ta
WHERE
	ta.id <> (
		SELECT
			min(tb.id)
		FROM
			dept AS tb
		WHERE
			ta. NAME = tb. NAME
	);
```


# 3. 删除MySQL重复行并保留id最小一行

```sql
-- 这种方法MySQL运行不行，SqlServer可以
DELETE ta
FROM
	dept AS ta
WHERE
	ta.id <> (
		SELECT
			maxId
		FROM
			(
				SELECT
					min(tb.id) AS maxId
				FROM
					dept AS tb
				WHERE
					ta.NAME = tb.NAME
			) AS t
	);



-- 下面这个方式对MySQL来说可以
DELETE ta
FROM
	dept AS ta
WHERE
	ta.id NOT IN (
		SELECT
			maxId
		FROM
			(
				SELECT
					min(tb.id) AS maxId
				FROM
					dept AS tb
				GROUP BY
					tb. NAME
			) AS t
	);

```
