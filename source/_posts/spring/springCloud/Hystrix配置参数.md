---
title: Hystrix配置参数
date: 2020-07-20
categories: ['SpringBoot']
tags: ['Hystrix','SpringCloud']
comments: true
id: HystrixConfig
---

#1. 官网地址
https://github.com/Netflix/Hystrix/wiki/Configuration#CommandCircuitBreaker

#2. 配置参数

#2.1 断路器 Circuit Breaker

| 参数名称                                 | 参数含义                                                                       | 参数默认值 |
| ---------------------------------------- | ------------------------------------------------------------------------------ | ---------- |
| circuitBreaker.enabled                   | 是否打开断路器                                                                 | true       |
| circuitBreaker.requestVolumeThreshold    | 滚动窗口内激活断路器的最小请求数量                                             | 20         |
| circuitBreaker.sleepWindowInMilliseconds | 此属性设置电路跳闸后拒绝请求的时间，然后允许再次尝试确定是否应再次闭合电路。   | 5000       |
| circuitBreaker.errorThresholdPercentage  | 此属性设置错误百分比，电路应在该百分比或以上跳闸，并启动对后备逻辑的短路请求。 | 50         |
| circuitBreaker.forceOpen                 | 强制打开断路器，优先级高于forceClosed                                          | false      |
|           circuitBreaker.forceClosed                               |                              强制关闭断路器                                                  |      false      |
