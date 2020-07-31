---
title: Redis数据结构-DICT
date: 2020-06-14
categories: ['Redis']
tags: ['Redis','DICT']
comments: true
id: redisData-DICT
---

# 1. Redis中字典的用处

-   redis数据库就是一个大的字典
-   哈希键的底层实现之一（当哈希键包含的键值对比较多，又或者键值对的元素都是较长的字符串值时）

# 2. 字典的数据结构实现

```C
/**
 * 哈希表的实现
 */
typedef stuct dictht {

  // 哈希表数组
  dictEntry **table;

  // 哈希表大小
  unsigned long size;

  // 哈希表大小掩码，计算索引值， 等于  size - 1
  unsigned long sizemark;

  // 该哈希表已有节点的数量
  unsigned long used;
}
```

```C
/**
 * 哈希节点的实现
 */
typedef stuct dictEntry {

  // 键
  void *key;

  // 值
  union {
    void *val;
    uint64_tu64;
    int64_tu64;
  } v;

  // 指向下一个哈希表节点，形成链表
  struct dictEntry *next;
}
```

```C
/**
 * 字典的实现
 */
typedef stuct dict {

  // 类型特定函数
  // 每个dictType结构保存了一簇用于操作特定类型键值对的函数。
  // redis会为用途不同的字典设置不同的类型特定函数。
  dictType *type;

  // 私有数据
  // 保存了需要传给类型特定函数的可选参数
  void *privData;

  // 哈希表
  // 包含两个dictht项，一般情况下只会用到ht[0]，ht[1]哈希表只会在对ht[0]哈希表进行rehash时使用
  dictht ht[2];

  // 记录了rehash的进度
  // 当rehash不在进行时，值为-1
  int rehashidx;
} dict
```


```C
/**
 * 字典的实现
 */
typedef stuct dictType {

  // 计算哈希值的函数
  unsigned int (*hashFunction))(const void *key);

  // 复制键的函数
  void *(*keyDup) (void *privData, const void *key);

  // 复制值的函数
  void *(*keyDup) (void *privData, const void *obj);

  // 对比键的函数
  void (*keyCompare) (void *privData, const void *key1, const void *key2);

  // 销毁键的函数
  void (*keyDestructor) (void  *privData, void *key);

  // 销毁值的函数
  void (*valueDestructor) (void  *privData, void *obj);
} dictType
```

# 3.
