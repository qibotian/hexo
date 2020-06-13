---
title: Redis实现分布式锁
date: 2020-05-27
categories: ['Redis']
tags: [Redis','分布式锁','setNx','RedLock']
comments: true
id: useRedisDoDistributeLock
---

-   redis 实现分布式锁，主要是通过setNx命令实现的。 实际项目中主要有以下几种实现方式，每种实现方式都有自己的优缺点。

# 1. 通过 RedisTemplate实现

```java
  final String lockValue = UUID.randomUUID().toString();

// redisTemplate 第一种实现方式， 缺点是设置值和设置过期时间不在同一事物中，如果设置值成功，但是设置过期方式失败，则可能发生死锁。
  boolean lock = stringRedisTemplate.opsForValue().setIfAbsent(goodsKey.getKey(), lockValue);
  stringRedisTemplate.expire(goodsKey.getKey(), goodsKey.getExpire(), goodsKey.getExpireTimeUnit());

// redisTemplate 第二种实现方式，在SpringBoot2.1版本或以上可以实现将设置值和过期时间放在同一事务中， 避免了死锁的发生，
// 但是此时仍会有一种可能性，即，设置了30秒的超时时间，但是可能整个业务处理的时间超过了30秒，导致了锁自动释放了，别的线程也就可以访问共享线程了
// 要解决这个问题，需要一个检测程序去检测，当前业务是否运行完成，如果没有运行完成，则将锁的时间再次延长，这也是Redisson锁实现的原理。
  boolean lock = stringRedisTemplate.opsForValue().setIfAbsent(goodsKey.getKey(), lockValue, goodsKey.getExpire(), goodsKey.getExpireTimeUnit());
  if(lock) {
    try {
      miaosha(dto);
    } finally {
      String cacheLockValue = (String) stringRedisTemplate.opsForValue().get(goodsKey.getKey());
      if(lockValue.equals(cacheLockValue)) {
        stringRedisTemplate.delete(goodsKey.getKey());
      }
    }
  }
```

# 2. 通过 redisson 实现

```java
// 使用redisson实现分布式事务锁， 避免了上述所说的锁超时问题，但是仍会出现以下问题
// 但是1： 如果主从结构，在master上设置锁成功了，但是尚未同步到slave节点时，master节点挂了，也会出现超卖问题 解决方案：RedLock
// 但是2：  单线程串行实现会有性能问题  解决方案： 使用分段锁，使不同段位落在不同的redis节点上
RLock lock = redissonClient.getLock(goodsKey.getKey());
lock.lock();
try {
  return  miaosha(dto);
} finally {
  lock.unlock();
}
```

# 3. 通过 RedLock 实现。

```java
// 使用RedLock实现分布式锁
// Redlock 实现原理是，只有集群中半数以上的节点加锁成功，才算加锁成功。 如果加锁失败，则需要回滚。
// 缺点1 ： 假如有5个节点ABCDE， 线程1 成功锁定了ABC 三个节点， 但是此时C节点挂了，导致C节点的数据没有来得及刷盘， 如果C节点重启，线程2又锁定了CDE三个节点，就会导致两个线程同时访问同一个共享资源。
// 解决方法： 延时重启，即节点挂了以后，不要立即重启，而是稍过一段时间重启。

// 参考文档 https://www.cnblogs.com/rgcLOVEyaya/p/RGC_LOVE_YAYA_1003days.html

Config config = new Config();
       config.useSentinelServers()
               .addSentinelAddress("127.0.0.1:6379","127.0.0.1:6389", "127.0.0.1:6399")
               .setMasterName("master")
               .setPassword("password")
               .setDatabase(0);
 RedissonClient client = Redisson.create(config);
 RLock lock = client.getLock(goodsKey.getKey());
 RLock lock2 = client.getLock(goodsKey.getKey());
 RLock lock3 = client.getLock(goodsKey.getKey());
 RedissonRedLock redLock = new RedissonRedLock(lock, lock2, lock3);
 try {
   boolean hasLock = redLock.tryLock(500, TimeUnit.MICROSECONDS);
   if(hasLock) {
       return  miaosha(dto);
   }
} catch (InterruptedException e) {
   e.printStackTrace();
} finally {
   redLock.unlock();
}
```
