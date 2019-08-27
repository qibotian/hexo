---
title: jmeter入门(3) beanShell脚本
date: 2019-08-23
categories: ['工具']
tags: ['jmeter']
comments: true
---

# 前言

# Bean Shell 内置遍历大全

  * log  打印日志，写入信息到jmeber.log文件。
  * SampleResult 获取SampleResult对象，能通过这个对象获取想要的信息。
  * Response 获取Response对象，能通过这个对象获取响应信息。
  * Failure 查看接口调使用能否成功，假如返回false是成功的，true是失败的。
  * FailureMessage 失败信息，没有设置的时候失败信息是空的，能set这个信息。
  * ResponseData 获取response body类型是byte[]。
  * ResponseCode 返回接口code成功是200。
  * ResponseMessage 获取msg成功是OK。
  * ResponseHeaders 获取接口服务端返回的头部信息。
  * RequestHeaders 获取用户端请求的头部信息。
  * SampleLabel 获取接口请求的名称。
  * SamplerData 获取请求的url和body。
  * ctx 代表上下文信息，能直接用。
  * vars即JMeterVariables，操作jmeter变量，这个变量实际引用了JMeter线程中的局部变量容器（本质上是Map），常用方法：
    * vars.get(String key)：从jmeter中获得变量值；
    * vars.put(String key，String value)：数据存到jmeter变量中；
  * prev 获取前面的sample返回的信息，常用方法：
    * getResponseDataAsString()：获取响应信息。
    * getResponseCode() ：获取响应code。

# 示例：

  ## 场景

    我们假设一个这样的场景，在发送请求时，我们先对请求体进行加密，请求返回后，我们需要对请求体进行解密。

  ## 具体步骤

    首先我们
