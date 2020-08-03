---
title: git多账户配置
id: gitAccountConfig
date: 2020-08-03
categories: ['工具']
tags: ['git']
comments: true
---

[TOC]

###1. 首先生成公私钥对

```bash
$ ssh-keygen -t rsa -C "自己的邮箱"
Generating public/private rsa key pair.
# 这里会让你输入生成的rsa文件名称,这里假如我们输入id_company
Enter file in which to save the key (/c/Users/xxx/.ssh/id_rsa):
# 这里会提示你输入密码和确认密码，这里直接回车就可以
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in id_company.
Your public key has been saved in id_company.pub.
The key fingerprint is:
SHA256:zUFNJve8UOkK2jIfxxxxxxxxxxxxxxxxhgVxg+lmny6Aw xxxxx.com.cn
The key\'s randomart image is:
+---[RSA 2048]----+
|  o.+*.   oo+ .. |
| . ooo.  . +.+.  |
|  . B  .  . ..o  |
|   * .. .o.. ... |
|E . .. oSoo. ..  |
| +    + = o .    |
|  o  . = + o     |
|      +.B o      |
|     ..=o=       |
+----[SHA256]-----+
```
###2. 重复上面步骤，将rsa文件名设置为另一个名字，比如id_home

###3. 在.ssh目录下新建一个config文件，内容如下
```
#公司的git
HOST git@自己公司的git地址
  User 用户名
  Hostname git@自己公司的git地址
  IdentityFile ~/.ssh/id_company
  #Port *** 公司的GIT端口

# 自己的地址
HOST git@自己的git地址
  User 用户名
  Hostname git@自己的git地址
  IdentityFile ~/.ssh/id_home
  #Port *** 自己的git端口
```

###4. 然后我们运行以下命令，将我们的账号假如know_hosts文件中：

```bash
$ ssh-agent bash
$ ssh-add ~/.ssh/id_company
$ ssh-add ~/.ssh/id_home

```
###5. 在响应的git库中将自己的公钥维护上去
