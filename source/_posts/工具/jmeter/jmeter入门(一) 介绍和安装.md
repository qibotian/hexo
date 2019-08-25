---
title: jmeter入门(一) 介绍和安装
date: 2019-08-23
categories: ['工具']
tags: ['jmeter']
comments: true
---

# jemter 官网地址

  https://jmeter.apache.org/

# jmeter 介绍

  jmeter是一款纯java开发的用于做 功能测试 和性能测试 的开源软件。它最初是为了测试web应用程序而设计的，后来逐渐扩展到其他应用程序。

  ![jmeter入门(一) 介绍和安装](what_is_jmeter.png)

# jmeter 可以用来做什么

  Apache JMeter 可以用来测试静态和动态资源以及web应用程序的性能。他可以用来模拟 服务器,服务器组，网络或者对象上的重负载(heavy load) ,以测试其健壮性（strength）或者分析其在不同负载类型（load type）情况下的整体性能(overall performance)。

  JMeter 有以下几种特性(features):  
  * 可以用来加载和测试许多种不同的应用程序（application）/服务(server)/协议类型(protocal type)..
    * WEB-HTTP, HTTPS(java, NodeJs, PHP, APS.NET)
    * SOAP/REST Webservices
    * FTP
    * Database via JDBC
    * LDAP
    * Message-oriented middleware (MOM) via JMS
    * Mail - SMTP(S), POP3(S) and IMAP(S)
    * Native commands or shell scripts
    * TCP
    * Java Objects
  * 功能齐全的IDE：允许快速记录（record），构建(build)，和调试(debug)测试计划。
  * 客户端模式（CLI model）可以从任何java友好操作系统(Java compatible OS)加载测试。
  * 一个完整的，随时可以呈现的HTML报告(HTML report)
  * 通过从当前流行的响应格式(HTML, JSON, XML或任何文本格式)中提取数据，可以用来很简单关联测试（Easy Correlation）
  * 高可移植性(Complete Portability), 纯Java(100% Java purity)
  * 多线程框架， 允许多线程同时(concurrent)取样，也允许多个线程组同时对不同的功能取样
  * 可缓存（cache），脱机分析/重放(offline analysis/replaying) 测试结果。
  * 高可扩展(Hightly Extensible)性:
    * 可插拔采样器 (Pluggable Sampler)，允许无限的测试能力
    * 脚本话采样器 (Scriptabel Sampler)。
    * 可插拔计时器（Pluggable timer），允许选择多个负载统计数据（Several load statistics）
    * 数据分析和可视化插件（Visualization plugin）有强大的个性化定制(personalzation)和扩展能力(great extensibility)。
    * 可以使用函数（Function）进行动态参数化，或者生产参数
    * 可以使用Maven, Gradle, Jenkins第三方开源库轻松的持续集成(Continuous Integration)。

# JMeter 下载及安装
  可以通过点击 [官网下载页面](https://jmeter.apache.org/download_jmeter.cgi) 直接下载最新的JMeter安装包。  

  * 下载完后，我们将得到的是一个免安装的压缩包，解压这个压缩包

  ![JMeter 下载页面](Jmeter_download.png)

  * 下载完后，我们将得到的是一个免安装的压缩包,我们解压后得到以下文件：  
  ![JMeter 文件列表](Jmeter_file_list.png)

  * 首先我们得确保我们本地的jdk环境在1.8或以上，我们在CMD上运行 `java -version` 查看jdk版本。  
  ![查看jdk版本](Jdk_version.png)

  * 我们双击JMeter安装目录下 `bin\ApacheJMeter.jar`,即可运行JMeter。当然在windowns下，我们也可以双击`bin\jmeter.bat`文件运行JMeter。  
  ![JMeter 运行文件](Bin_apacheJMeter.png)

  * JMeter首页  
  ![JMeter 首页](Jmeter_index.png)

# 下章节内容
  在下一章节，我们将介绍如何使用JMeter进行测试用例的录制(record)。
