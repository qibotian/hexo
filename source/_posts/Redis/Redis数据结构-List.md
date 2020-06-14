---
title: Redis数据结构-List
date: 2020-05-27
categories: ['Redis']
tags: [Redis','List']
comments: true
id: redisData-ListNode
---

# 1. Redis中List的用处。

1.  列表键的底层实现（当列表键的元素比较多时，或者元素都是比较长的字符串时）
2.  发布与订阅，慢查询，监视器等功能也使用了链表。
3.  服务器本身使用链表来保存客户端信息，客户端的输出缓冲区等。

# 2. 节点和列表数据结构定义

```C
/**
 * 节点的定义
 */
typedef struct ListNode {

  // 前置节点
  struct ListNode *prev;

  // 后置节点
  struct ListNode *next;

  //节点的值
  void *value;

}
```

```C
/**
 * 列表的定义
 */
typedef struct ListNode {

  // 头结点
  struct ListNode *head;

  // 尾节点
  struct ListNode *tail;

  //节点的值
  unsigned long len;

  //节点复制函数
  void *(*(dup)) (void *ptr);

  //节点释放函数
  void *(*(free)) (void *ptr);

  //节点对比函数
  void *(*(match)) (void *ptr, void *key);

}
```

# 3. List的特性

* 双端链表：每个节点都有prev 和 next节点，获取某个节点的前置节点和后置节点的复杂度都是O(1)；
* 无环： 表头节点的prev 和 表尾节点都指向NULL，对链表的访问以NULL为终点。
* 带表头节点和表尾节点： 获取表头或者表尾的复杂度都是O(1)
* 带链表长度： 获取长度复杂度为O(1)
* 多态：链表节点使用void*指针来保存节点的值，可以用来保存不同类型的值。

# 4. 示例
![](http://qiniu.yangrouhubo.com/markdown-img-paste-20200614193540272.png)
