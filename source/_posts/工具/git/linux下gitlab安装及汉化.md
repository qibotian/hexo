---
title: linux下gitlab安装及汉化
id: install_gitlab
date: 2020-07-31
categories: ['工具']
tags: ['git']
comments: true
---

```**bash**
# 安装依赖

$ yum install -y curl policycoreutils openssh-server openssh-clients policycoreutils-python
$ systemctl enable sshd
$ systemctl start sshd

# 使用postfix发送邮件通知
$ yum install -y postfix
$ systemctl enable postfix
$ systemctl start postfix
# 这个时候启动会报错    postfix[5181]: fatal: parameter inet_interfaces: no local     interface found for ::1
# 修改/etc/postfix/main.cf文件中  inet_interfaces = localhost 为 inet_interfaces = all
# 然后重新启动


# 打开防火墙端口，如果需要
$ systemctl start firewalld
$ firewall-cmd --permanent --add-service=http
$ systemctl reload firewalld


# 下载安装包
$ wget https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el7/gitlab-ce-11.4.6-ce.0.el7.x86_64.rpm

# 安装gitlab
$ rpm -ivh gitlab-ce-11.4.6-ce.0.el7.x86_64.rpm

$ sudo vim /etc/gitlab/gitlab.rb
# 指定访问的端口
# external_url 'http://127.0.0.1:12345'


# 重启gitlab
$ gitlab-ctl reconfigure

# 开启防火墙和端口映射即可访问
# 启动防火墙
$ sudo systemctl start firewalld
# 查看防火墙
$ firewall-cmd --state
# 列出开放的端口
$ firewall-cmd --list-ports
# 将指定端口加入防火墙
$ firewall-cmd --zone=public --add-port=12345/tcp --permanent
# 重启防火墙
$ firewall-cmd --reload

# 访问 http://127.0.0.1:12345/

#汉化

# 先停止gitlab
$ sudo gitlab-ctl stop

#下载汉化项目
$ git clone https://gitlab.com/xhang/gitlab.git
# 如果下载速度特别慢，我这里找了一个gitee的项目
$ git clone https://gitee.com/panda26/gitlab.git

## 进入克隆的项目中
$ cd gitlab

## 查看版本，如果是和我一样配置的话，那版本号就是 11.4.6
$ head -1 /opt/gitlab/version-manifest.txt

## 生成差异文件
$ git diff v11.4.6 v11.4.6-zh > ../11.4.6-zh.diff

## 把差异文件打补丁

$ sudo yum install patch -y
$ sudo patch -d /opt/gitlab/embedded/service/gitlab-rails -p1 < ../11.4.6.diff

## 重启gitlab
$ sudo gitlab-ctl start

## 重新刷下配置
$ sudo gitlab-ctl reconfigure









```
