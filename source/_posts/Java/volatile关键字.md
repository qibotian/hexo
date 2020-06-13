---
title: volatile关键字
date: 2019-05-17
categories: ['volatile','JAVA']
tags: ['Java']
comments: true
id: javavolatile
---

volatile 关键字的作用和用法

<!--more-->

# java的内存模型

Java内存的模型规定了，所有的共享变量都存储在主内存中，每个线程都有自己的工作内存，线程的工作内存保存该线程使用到的主内存中的变量的一个Copy,线程对所有变量的操作都是基于这个COPY的，而不能直接读写主存中的变量。不同线程之间无法直接访问对方的工作内存中变量，线程之间的变量值传递都需要在主内存中完成。

# 什么是指令重排


# volatile的作用

# volatile的用法
