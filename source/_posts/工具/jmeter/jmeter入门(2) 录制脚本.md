---
title: jmeter入门(2) 录制脚本
date: 2019-08-23
categories: ['工具']
tags: ['jmeter']
comments: true
---

# 前言

  有的时候，我们需要录制请求的脚本。而JMeter也为我们提供了这样的功能。下面我们简单介绍下用JMeter录制脚本方法。

# 准备工作

  * 博主用的是JMeter5版本的JMeter
  * Chrome浏览器
  * Chrome浏览器安装了[SwitchyOmega](https://github.com/FelisCatus/SwitchyOmega)扩展程序。

## 模拟场景

  假如我们现在需要录制[百度搜索](https://www.baidu.com)的相关api。

# 开始

## 第一步，我们新建一个录制脚本的测试计划。

  * 点击 `文件` ,选择 `模板` 。
  * 在弹出界面上方中的 `Select Templete` 中，选择 `Recording`
  * 点击下方 `Create` 按钮。
  * 在下来的界面中依次输入
    * 站点(hostToRecord) : www.baidu.com
    * 录制脚本输出文件(recordOutputFile): recording.xml
    * 录制协议(schemeToRecord): https
  * 点击下方 `Create` 按钮。

  ![新建录制脚本测试计划](Create_record_test_sampler.gif)

## 第二步，打开代理

  
