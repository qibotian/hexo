---
title: linux安装git
id: install_git
date: 2020-07-31
categories: ['工具']
tags: ['git']
comments: true
---

```
# 移除自带的git

yum remove git

# 下载git

 wget https://github.com/git/git/archive/v2.17.0.tar.gz

# 解压

 tar -zxvf v2.17.0.tar.gz

# 安装依赖并编译

yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel gcc perl-ExtUtils-MakeMaker

# 安装

 cd git-2.17.0
 make prefix=/usr/local/git all

# 设置安装路径

  make prefix=/usr/local/git install

# 配置环境变量

vim /etc/profile
在文件底部加上：

PATH=$PATH:/usr/local/git/bin
export PATH

# 查看版本

git --version

## 如果显示仍为旧版本，则重新打开个终端试试。




```
