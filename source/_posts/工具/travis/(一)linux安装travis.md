---
title: (一)linux安装travis
date: 2019-08-16
categories: ['工具']
tags: ['travis ci','自动集成','travis', 'gem']
comments: true
---

```
┌────────────────────────────────────────────────────────────────────┐
│                        • MobaXterm 11.1 •                          │
│            (SSH client, X-server and networking tools)             │
│                                                                    │
│ ➤ SSH session to root@qbt.91biz.com.cn                             │
│   • SSH compression : ✔                                            │
│   • SSH-browser     : ✔                                            │
│   • X11-forwarding  : ✘  (disabled or not supported by server)     │
│   • DISPLAY         : 10.2.9.9:0.0                                 │
│                                                                    │
│ ➤ For more info, ctrl+click on help or visit our website           │
└────────────────────────────────────────────────────────────────────┘

Last failed login: Sat May  9 14:36:17 CST 2020 from 176.253.4.88 on ssh:notty
There were 46 failed login attempts since the last successful login.
Last login: Sun May  3 12:34:50 2020 from 111.197.22.128

Welcome to Alibaba Cloud Elastic Compute Service !

[root@daluobo ~]#
[root@daluobo ~]# useradd travis
[root@daluobo ~]# passwd travis
Changing password for user travis.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
[root@daluobo ~]# vim /etc/sudo
sudo.conf       sudoers         sudoers.d/      sudo-ldap.conf
[root@daluobo ~]# vim /etc/sudo
sudo.conf       sudoers         sudoers.d/      sudo-ldap.conf
[root@daluobo ~]# vim /etc/sudoers
[root@daluobo ~]# su travis
[travis@daluobo root]$ cd ~
[travis@daluobo ~]$ ssh-ketgen -t rsa
bash: ssh-ketgen: command not found
[travis@daluobo ~]$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/home/travis/.ssh/id_rsa):
Created directory '/home/travis/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/travis/.ssh/id_rsa.
Your public key has been saved in /home/travis/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:X+A1VBF4o+Y0GOL4V+8u2dJlxkdXRAAzzO/Os3DPnBQ travis@daluobo
The key's randomart image is:
+---[RSA 2048]----+
|           o=+=*o|
|        . ..+oo .|
|       o ..oo+ ..|
|      . ...o*.. o|
|       .S .=.+ E.|
|        ..... o B|
|         .. .B.=.|
|            +oO+.|
|             +o++|
+----[SHA256]-----+
[travis@daluobo ~]$
[travis@daluobo ~]$ cd /home/travis
[travis@daluobo ~]$ ls
[travis@daluobo ~]$ chmod 700 ~/.ssh/*
[travis@daluobo ~]$ chmod 700 ~/.ssh/
[travis@daluobo ~]$ chmod 600 ~/.ssh/*
[travis@daluobo ~]$ ls -la
total 24
drwx------  3 travis travis 4096 May  9 17:23 .
drwxr-xr-x. 4 root   root   4096 May  9 17:19 ..
-rw-r--r--  1 travis travis   18 Aug  8  2019 .bash_logout
-rw-r--r--  1 travis travis  193 Aug  8  2019 .bash_profile
-rw-r--r--  1 travis travis  231 Aug  8  2019 .bashrc
drwx------  2 travis travis 4096 May  9 17:23 .ssh
[travis@daluobo ~]$ cd .ssh/
[travis@daluobo .ssh]$ ls
id_rsa  id_rsa.pub
[travis@daluobo .ssh]$ ls -la
total 16
drwx------ 2 travis travis 4096 May  9 17:23 .
drwx------ 3 travis travis 4096 May  9 17:23 ..
-rw------- 1 travis travis 1679 May  9 17:23 id_rsa
-rw------- 1 travis travis  396 May  9 17:23 id_rsa.pub
[travis@daluobo .ssh]$ cat id_rsa.pub >> authorized_keys
[travis@daluobo .ssh]$ cat authorized_keys
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDe+CJrrwl9PNgEnbGwNHGq2HiKyIRID3DNRlz++sdZf9mVp2UZMUmTp8TiQwf52fgSywjuYR                                                                                      WoR4iiLFge13TK46iRSCTxPYJ7VfCkGP5GgLUME9WBKldiT6DhtmDni/negskebahpeNJKT4Wgw08BC7MRq/emIcQfJzCoXfw9KPZHXiEKAzrp                                                                                      aue6mjluG7gxG4taDMsxCf5n5FyrWhaEOffr5B/apAR+0WcfU4W2rgB6b231UkLiQS54dgvam4z3kFFpUgy+gGwsyhYgMPwMqAYCPp/DX5xt+1                                                                                      kE/WR0vQ7Yz8cLT8MlP5a/N1n+NJZXWib72m4iq1Ba5KeqZXEB travis@daluobo
[travis@daluobo .ssh]$ vim config
[travis@daluobo .ssh]$
[travis@daluobo .ssh]$ curl -sSL https://get.rvm.io | bash -s stable
curl: (7) Failed connect to api.github.com:443; Connection refused
WARN: ...the preceeding error with code 7 occurred while fetching https://api.github.com/repos/rvm/rvm/tags
Downloading https://github.com/rvm/rvm/archive/1.29.10.tar.gz
^C
[travis@daluobo .ssh]$ gem -v
bash: gem: command not found
[travis@daluobo .ssh]$
[travis@daluobo .ssh]$ curl -sSL https://get.rvm.io | bash -s stable
curl: (7) Failed connect to raw.githubusercontent.com:443; Connection refused
[travis@daluobo .ssh]$ gem
bash: gem: command not found
[travis@daluobo .ssh]$ ruby -v
bash: ruby: command not found
[travis@daluobo .ssh]$ yum -y install ruby ruby-devel rubygems rpm-build
Loaded plugins: fastestmirror
You need to be root to perform this command.
[travis@daluobo .ssh]$ su root
Password:
su: Authentication failure
[travis@daluobo .ssh]$ su root
Password:
[root@daluobo .ssh]# yum -y install ruby ruby-devel rubygems rpm-build
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
* base: mirrors.cloud.aliyuncs.com
* extras: mirrors.cloud.aliyuncs.com
* updates: mirrors.cloud.aliyuncs.com
* webtatic: us-east.repo.webtatic.com
base                                                                                   | 3.6 kB  00:00:00
epel                                                                                   | 4.7 kB  00:00:00
extras                                                                                 | 2.9 kB  00:00:00
updates                                                                                | 2.9 kB  00:00:00
webtatic                                                                               | 3.6 kB  00:00:00
(1/7): base/7/x86_64/group_gz                                                          | 153 kB  00:00:00
(2/7): epel/x86_64/group_gz                                                            |  95 kB  00:00:00
(3/7): epel/x86_64/updateinfo                                                          | 1.0 MB  00:00:00
(4/7): base/7/x86_64/primary_db                                                        | 6.1 MB  00:00:00
(5/7): epel/x86_64/primary_db                                                          | 6.8 MB  00:00:00
(6/7): extras/7/x86_64/primary_db                                                      | 190 kB  00:00:00
(7/7): updates/7/x86_64/primary_db                                                     | 176 kB  00:00:00
Resolving Dependencies
--> Running transaction check
---> Package rpm-build.x86_64 0:4.11.3-43.el7 will be installed
--> Processing Dependency: rpm = 4.11.3-43.el7 for package: rpm-build-4.11.3-43.el7.x86_64
--> Processing Dependency: elfutils >= 0.128 for package: rpm-build-4.11.3-43.el7.x86_64
--> Processing Dependency: system-rpm-config for package: rpm-build-4.11.3-43.el7.x86_64
--> Processing Dependency: bzip2 for package: rpm-build-4.11.3-43.el7.x86_64
--> Processing Dependency: /usr/bin/gdb-add-index for package: rpm-build-4.11.3-43.el7.x86_64
---> Package ruby.x86_64 0:2.0.0.648-36.el7 will be installed
--> Processing Dependency: ruby-libs(x86-64) = 2.0.0.648-36.el7 for package: ruby-2.0.0.648-36.el7.x86_64
--> Processing Dependency: rubygem(bigdecimal) >= 1.2.0 for package: ruby-2.0.0.648-36.el7.x86_64
--> Processing Dependency: libruby.so.2.0()(64bit) for package: ruby-2.0.0.648-36.el7.x86_64
---> Package ruby-devel.x86_64 0:2.0.0.648-36.el7 will be installed
---> Package rubygems.noarch 0:2.0.14.1-36.el7 will be installed
--> Processing Dependency: rubygem(rdoc) >= 4.0.0 for package: rubygems-2.0.14.1-36.el7.noarch
--> Processing Dependency: rubygem(psych) >= 2.0.0 for package: rubygems-2.0.14.1-36.el7.noarch
--> Processing Dependency: rubygem(io-console) >= 0.4.2 for package: rubygems-2.0.14.1-36.el7.noarch
--> Running transaction check
---> Package bzip2.x86_64 0:1.0.6-13.el7 will be installed
---> Package elfutils.x86_64 0:0.176-4.el7 will be installed
--> Processing Dependency: elfutils-libs(x86-64) = 0.176-4.el7 for package: elfutils-0.176-4.el7.x86_64
--> Processing Dependency: elfutils-libelf(x86-64) = 0.176-4.el7 for package: elfutils-0.176-4.el7.x86_64
---> Package gdb.x86_64 0:7.6.1-119.el7 will be installed
---> Package redhat-rpm-config.noarch 0:9.1.0-88.el7.centos will be installed
--> Processing Dependency: dwz >= 0.4 for package: redhat-rpm-config-9.1.0-88.el7.centos.noarch
--> Processing Dependency: python-srpm-macros for package: redhat-rpm-config-9.1.0-88.el7.centos.noarch
--> Processing Dependency: perl-srpm-macros for package: redhat-rpm-config-9.1.0-88.el7.centos.noarch
---> Package rpm.x86_64 0:4.11.3-40.el7 will be updated
--> Processing Dependency: rpm = 4.11.3-40.el7 for package: rpm-python-4.11.3-40.el7.x86_64
--> Processing Dependency: rpm = 4.11.3-40.el7 for package: rpm-libs-4.11.3-40.el7.x86_64
---> Package rpm.x86_64 0:4.11.3-43.el7 will be an update
---> Package ruby-libs.x86_64 0:2.0.0.648-36.el7 will be installed
---> Package rubygem-bigdecimal.x86_64 0:1.2.0-36.el7 will be installed
---> Package rubygem-io-console.x86_64 0:0.4.2-36.el7 will be installed
---> Package rubygem-psych.x86_64 0:2.0.0-36.el7 will be installed
---> Package rubygem-rdoc.noarch 0:4.0.0-36.el7 will be installed
--> Processing Dependency: ruby(irb) = 2.0.0.648 for package: rubygem-rdoc-4.0.0-36.el7.noarch
--> Processing Dependency: rubygem(json) >= 1.7.7 for package: rubygem-rdoc-4.0.0-36.el7.noarch
--> Running transaction check
---> Package dwz.x86_64 0:0.11-3.el7 will be installed
---> Package elfutils-libelf.x86_64 0:0.176-2.el7 will be updated
---> Package elfutils-libelf.x86_64 0:0.176-4.el7 will be an update
---> Package elfutils-libs.x86_64 0:0.176-2.el7 will be updated
---> Package elfutils-libs.x86_64 0:0.176-4.el7 will be an update
---> Package perl-srpm-macros.noarch 0:1-8.el7 will be installed
---> Package python-srpm-macros.noarch 0:3-32.el7 will be installed
---> Package rpm-libs.x86_64 0:4.11.3-40.el7 will be updated
--> Processing Dependency: rpm-libs(x86-64) = 4.11.3-40.el7 for package: rpm-build-libs-4.11.3-40.el7.x86_64
---> Package rpm-libs.x86_64 0:4.11.3-43.el7 will be an update
---> Package rpm-python.x86_64 0:4.11.3-40.el7 will be updated
---> Package rpm-python.x86_64 0:4.11.3-43.el7 will be an update
---> Package ruby-irb.noarch 0:2.0.0.648-36.el7 will be installed
---> Package rubygem-json.x86_64 0:1.7.7-36.el7 will be installed
--> Running transaction check
---> Package rpm-build-libs.x86_64 0:4.11.3-40.el7 will be updated
---> Package rpm-build-libs.x86_64 0:4.11.3-43.el7 will be an update
--> Finished Dependency Resolution

Dependencies Resolved

==============================================================================================================
Package                         Arch                Version                          Repository         Size
==============================================================================================================
Installing:
rpm-build                       x86_64              4.11.3-43.el7                    base              149 k
ruby                            x86_64              2.0.0.648-36.el7                 base               73 k
ruby-devel                      x86_64              2.0.0.648-36.el7                 base              133 k
rubygems                        noarch              2.0.14.1-36.el7                  base              215 k
Installing for dependencies:
bzip2                           x86_64              1.0.6-13.el7                     base               52 k
dwz                             x86_64              0.11-3.el7                       base               99 k
elfutils                        x86_64              0.176-4.el7                      base              308 k
gdb                             x86_64              7.6.1-119.el7                    base              2.4 M
perl-srpm-macros                noarch              1-8.el7                          base              4.6 k
python-srpm-macros              noarch              3-32.el7                         base              8.4 k
redhat-rpm-config               noarch              9.1.0-88.el7.centos              base               81 k
ruby-irb                        noarch              2.0.0.648-36.el7                 base               94 k
ruby-libs                       x86_64              2.0.0.648-36.el7                 base              2.8 M
rubygem-bigdecimal              x86_64              1.2.0-36.el7                     base               85 k
rubygem-io-console              x86_64              0.4.2-36.el7                     base               56 k
rubygem-json                    x86_64              1.7.7-36.el7                     base               81 k
rubygem-psych                   x86_64              2.0.0-36.el7                     base               84 k
rubygem-rdoc                    noarch              4.0.0-36.el7                     base              324 k
Updating for dependencies:
elfutils-libelf                 x86_64              0.176-4.el7                      base              195 k
elfutils-libs                   x86_64              0.176-4.el7                      base              291 k
rpm                             x86_64              4.11.3-43.el7                    base              1.2 M
rpm-build-libs                  x86_64              4.11.3-43.el7                    base              107 k
rpm-libs                        x86_64              4.11.3-43.el7                    base              278 k
rpm-python                      x86_64              4.11.3-43.el7                    base               84 k

Transaction Summary
==============================================================================================================
Install  4 Packages (+14 Dependent packages)
Upgrade             (  6 Dependent packages)

Total download size: 9.1 M
Downloading packages:
Delta RPMs disabled because /usr/bin/applydeltarpm not installed.
(1/24): bzip2-1.0.6-13.el7.x86_64.rpm                                                  |  52 kB  00:00:00
(2/24): dwz-0.11-3.el7.x86_64.rpm                                                      |  99 kB  00:00:00
(3/24): elfutils-0.176-4.el7.x86_64.rpm                                                | 308 kB  00:00:00
(4/24): elfutils-libs-0.176-4.el7.x86_64.rpm                                           | 291 kB  00:00:00
(5/24): elfutils-libelf-0.176-4.el7.x86_64.rpm                                         | 195 kB  00:00:00
(6/24): gdb-7.6.1-119.el7.x86_64.rpm                                                   | 2.4 MB  00:00:00
(7/24): perl-srpm-macros-1-8.el7.noarch.rpm                                            | 4.6 kB  00:00:00
(8/24): redhat-rpm-config-9.1.0-88.el7.centos.noarch.rpm                               |  81 kB  00:00:00
(9/24): python-srpm-macros-3-32.el7.noarch.rpm                                         | 8.4 kB  00:00:00
(10/24): rpm-4.11.3-43.el7.x86_64.rpm                                                  | 1.2 MB  00:00:00
(11/24): rpm-build-4.11.3-43.el7.x86_64.rpm                                            | 149 kB  00:00:00
(12/24): rpm-libs-4.11.3-43.el7.x86_64.rpm                                             | 278 kB  00:00:00
(13/24): rpm-python-4.11.3-43.el7.x86_64.rpm                                           |  84 kB  00:00:00
(14/24): rpm-build-libs-4.11.3-43.el7.x86_64.rpm                                       | 107 kB  00:00:00
(15/24): ruby-2.0.0.648-36.el7.x86_64.rpm                                              |  73 kB  00:00:00
(16/24): ruby-irb-2.0.0.648-36.el7.noarch.rpm                                          |  94 kB  00:00:00
(17/24): ruby-libs-2.0.0.648-36.el7.x86_64.rpm                                         | 2.8 MB  00:00:00
(18/24): rubygem-bigdecimal-1.2.0-36.el7.x86_64.rpm                                    |  85 kB  00:00:00
(19/24): ruby-devel-2.0.0.648-36.el7.x86_64.rpm                                        | 133 kB  00:00:00
(20/24): rubygem-io-console-0.4.2-36.el7.x86_64.rpm                                    |  56 kB  00:00:00
(21/24): rubygem-psych-2.0.0-36.el7.x86_64.rpm                                         |  84 kB  00:00:00
(22/24): rubygem-json-1.7.7-36.el7.x86_64.rpm                                          |  81 kB  00:00:00
(23/24): rubygem-rdoc-4.0.0-36.el7.noarch.rpm                                          | 324 kB  00:00:00
(24/24): rubygems-2.0.14.1-36.el7.noarch.rpm                                           | 215 kB  00:00:00
--------------------------------------------------------------------------------------------------------------
Total                                                                          11 MB/s | 9.1 MB  00:00:00
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
Installing : ruby-libs-2.0.0.648-36.el7.x86_64                                                         1/30
Updating   : elfutils-libelf-0.176-4.el7.x86_64                                                        2/30
Updating   : rpm-libs-4.11.3-43.el7.x86_64                                                             3/30
Updating   : rpm-4.11.3-43.el7.x86_64                                                                  4/30
Updating   : rpm-build-libs-4.11.3-43.el7.x86_64                                                       5/30
Updating   : elfutils-libs-0.176-4.el7.x86_64                                                          6/30
Installing : elfutils-0.176-4.el7.x86_64                                                               7/30
Installing : dwz-0.11-3.el7.x86_64                                                                     8/30
Installing : ruby-irb-2.0.0.648-36.el7.noarch                                                          9/30
Installing : ruby-2.0.0.648-36.el7.x86_64                                                             10/30
Installing : rubygem-bigdecimal-1.2.0-36.el7.x86_64                                                   11/30
Installing : rubygem-rdoc-4.0.0-36.el7.noarch                                                         12/30
Installing : rubygem-json-1.7.7-36.el7.x86_64                                                         13/30
Installing : rubygem-io-console-0.4.2-36.el7.x86_64                                                   14/30
Installing : rubygems-2.0.14.1-36.el7.noarch                                                          15/30
Installing : rubygem-psych-2.0.0-36.el7.x86_64                                                        16/30
Installing : gdb-7.6.1-119.el7.x86_64                                                                 17/30
Installing : python-srpm-macros-3-32.el7.noarch                                                       18/30
Installing : perl-srpm-macros-1-8.el7.noarch                                                          19/30
Installing : redhat-rpm-config-9.1.0-88.el7.centos.noarch                                             20/30
Installing : bzip2-1.0.6-13.el7.x86_64                                                                21/30
Installing : rpm-build-4.11.3-43.el7.x86_64                                                           22/30
Installing : ruby-devel-2.0.0.648-36.el7.x86_64                                                       23/30
Updating   : rpm-python-4.11.3-43.el7.x86_64                                                          24/30
Cleanup    : rpm-python-4.11.3-40.el7.x86_64                                                          25/30
Cleanup    : rpm-build-libs-4.11.3-40.el7.x86_64                                                      26/30
Cleanup    : rpm-4.11.3-40.el7.x86_64                                                                 27/30
Cleanup    : rpm-libs-4.11.3-40.el7.x86_64                                                            28/30
Cleanup    : elfutils-libs-0.176-2.el7.x86_64                                                         29/30
Cleanup    : elfutils-libelf-0.176-2.el7.x86_64                                                       30/30
Verifying  : rpm-build-4.11.3-43.el7.x86_64                                                            1/30
Verifying  : rubygem-psych-2.0.0-36.el7.x86_64                                                         2/30
Verifying  : rubygems-2.0.14.1-36.el7.noarch                                                           3/30
Verifying  : elfutils-libs-0.176-4.el7.x86_64                                                          4/30
Verifying  : bzip2-1.0.6-13.el7.x86_64                                                                 5/30
Verifying  : perl-srpm-macros-1-8.el7.noarch                                                           6/30
Verifying  : rpm-build-libs-4.11.3-43.el7.x86_64                                                       7/30
Verifying  : python-srpm-macros-3-32.el7.noarch                                                        8/30
Verifying  : ruby-2.0.0.648-36.el7.x86_64                                                              9/30
Verifying  : rpm-4.11.3-43.el7.x86_64                                                                 10/30
Verifying  : rubygem-rdoc-4.0.0-36.el7.noarch                                                         11/30
Verifying  : rubygem-bigdecimal-1.2.0-36.el7.x86_64                                                   12/30
Verifying  : elfutils-libelf-0.176-4.el7.x86_64                                                       13/30
Verifying  : ruby-irb-2.0.0.648-36.el7.noarch                                                         14/30
Verifying  : ruby-libs-2.0.0.648-36.el7.x86_64                                                        15/30
Verifying  : elfutils-0.176-4.el7.x86_64                                                              16/30
Verifying  : ruby-devel-2.0.0.648-36.el7.x86_64                                                       17/30
Verifying  : gdb-7.6.1-119.el7.x86_64                                                                 18/30
Verifying  : rpm-python-4.11.3-43.el7.x86_64                                                          19/30
Verifying  : dwz-0.11-3.el7.x86_64                                                                    20/30
Verifying  : rubygem-json-1.7.7-36.el7.x86_64                                                         21/30
Verifying  : rubygem-io-console-0.4.2-36.el7.x86_64                                                   22/30
Verifying  : rpm-libs-4.11.3-43.el7.x86_64                                                            23/30
Verifying  : redhat-rpm-config-9.1.0-88.el7.centos.noarch                                             24/30
Verifying  : rpm-build-libs-4.11.3-40.el7.x86_64                                                      25/30
Verifying  : rpm-python-4.11.3-40.el7.x86_64                                                          26/30
Verifying  : elfutils-libelf-0.176-2.el7.x86_64                                                       27/30
Verifying  : rpm-libs-4.11.3-40.el7.x86_64                                                            28/30
Verifying  : rpm-4.11.3-40.el7.x86_64                                                                 29/30
Verifying  : elfutils-libs-0.176-2.el7.x86_64                                                         30/30

Installed:
rpm-build.x86_64 0:4.11.3-43.el7    ruby.x86_64 0:2.0.0.648-36.el7   ruby-devel.x86_64 0:2.0.0.648-36.el7
rubygems.noarch 0:2.0.14.1-36.el7

Dependency Installed:
bzip2.x86_64 0:1.0.6-13.el7                              dwz.x86_64 0:0.11-3.el7
elfutils.x86_64 0:0.176-4.el7                            gdb.x86_64 0:7.6.1-119.el7
perl-srpm-macros.noarch 0:1-8.el7                        python-srpm-macros.noarch 0:3-32.el7
redhat-rpm-config.noarch 0:9.1.0-88.el7.centos           ruby-irb.noarch 0:2.0.0.648-36.el7
ruby-libs.x86_64 0:2.0.0.648-36.el7                      rubygem-bigdecimal.x86_64 0:1.2.0-36.el7
rubygem-io-console.x86_64 0:0.4.2-36.el7                 rubygem-json.x86_64 0:1.7.7-36.el7
rubygem-psych.x86_64 0:2.0.0-36.el7                      rubygem-rdoc.noarch 0:4.0.0-36.el7

Dependency Updated:
elfutils-libelf.x86_64 0:0.176-4.el7  elfutils-libs.x86_64 0:0.176-4.el7 rpm.x86_64 0:4.11.3-43.el7
rpm-build-libs.x86_64 0:4.11.3-43.el7 rpm-libs.x86_64 0:4.11.3-43.el7    rpm-python.x86_64 0:4.11.3-43.el7

Complete!
[root@daluobo .ssh]#
[root@daluobo .ssh]# gem -v
2.0.14.1
[root@daluobo .ssh]#
[root@daluobo .ssh]# gem sources --add https://gems.ruby-china.org/ --remove https://rubygems.org/
Error fetching https://gems.ruby-china.org/:
   bad response Not Found 404 (https://gems.ruby-china.org/specs.4.8.gz)
[root@daluobo .ssh]# https://gems.ruby-china.org/ added to sources
bash: https://gems.ruby-china.org/: No such file or directory
[root@daluobo .ssh]# https://rubygems.org/ removed from sources
bash: https://rubygems.org/: No such file or directory
[root@daluobo .ssh]# gem install travis


^CERROR:  Interrupted
[root@daluobo .ssh]# gem sources
*** CURRENT SOURCES ***

https://rubygems.org/
[root@daluobo .ssh]# gem sources -a http://mirrors.aliyun.com/rubygems/
http://mirrors.aliyun.com/rubygems/ added to sources
Killed
[root@daluobo .ssh]# gem sources -r https://rubygems.org/
https://rubygems.org/ removed from sources
[root@daluobo .ssh]# gem sources -u
source cache successfully updated
[root@daluobo .ssh]# gem install travis
Fetching: multipart-post-2.1.1.gem (100%)
Successfully installed multipart-post-2.1.1
Fetching: faraday-1.0.1.gem (100%)
ERROR:  Error installing travis:
   faraday requires Ruby version >= 2.3.
[root@daluobo .ssh]# gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3                                                                                       7D2BAF1CF37B13E2069D6956105BD0E739499BDB
gpg: directory `/root/.gnupg' created
gpg: new configuration file `/root/.gnupg/gpg.conf' created
gpg: WARNING: options in `/root/.gnupg/gpg.conf' are not yet active during this run
gpg: keyring `/root/.gnupg/secring.gpg' created
gpg: keyring `/root/.gnupg/pubring.gpg' created
gpg: requesting key D39DC0E3 from hkp server keys.gnupg.net
gpg: requesting key 39499BDB from hkp server keys.gnupg.net
gpg: /root/.gnupg/trustdb.gpg: trustdb created
gpg: key D39DC0E3: public key "Michal Papis (RVM signing) <mpapis@gmail.com>" imported
gpg: key 39499BDB: public key "Piotr Kuczynski <piotr.kuczynski@gmail.com>" imported
gpg: no ultimately trusted keys found
gpg: Total number processed: 2
gpg:               imported: 2  (RSA: 2)
[root@daluobo .ssh]# curl -sSL https://get.rvm.io | bash -s stable
curl: (7) Failed connect to api.github.com:443; Connection refused
WARN: ...the preceeding error with code 7 occurred while fetching https://api.github.com/repos/rvm/rvm/tags
Downloading https://github.com/rvm/rvm/archive/1.29.10.tar.gz
Downloading https://github.com/rvm/rvm/releases/download/1.29.10/1.29.10.tar.gz.asc
gpg: Signature made Thu 26 Mar 2020 05:58:42 AM CST using RSA key ID 39499BDB
gpg: Good signature from "Piotr Kuczynski <piotr.kuczynski@gmail.com>"
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: 7D2B AF1C F37B 13E2 069D  6956 105B D0E7 3949 9BDB
GPG verified '/usr/local/rvm/archives/rvm-1.29.10.tgz'
Creating group 'rvm'
Installing RVM to /usr/local/rvm/
Installation of RVM in /usr/local/rvm/ is almost complete:

* First you need to add all users that will be using rvm to 'rvm' group,
and logout - login again, anyone using rvm will be operating with `umask u=rwx,g=rwx,o=rx`.

* To start using RVM you need to run `source /etc/profile.d/rvm.sh`
in all your open shell windows, in rare cases you need to reopen all shell windows.
* Please do NOT forget to add your users to the rvm group.
The installer no longer auto-adds root or users to the rvm group. Admins must do this.
Also, please note that group memberships are ONLY evaluated at login time.
This means that users must log out then back in before group membership takes effect!
Thanks for installing RVM 🙏
Please consider donating to our open collective to help us maintain RVM.

👉  Donate: https://opencollective.com/rvm/donate


[root@daluobo .ssh]# source /etc/profile.d/rvm.sh
[root@daluobo .ssh]# rvm list known
# MRI Rubies
[ruby-]1.8.6[-p420]
[ruby-]1.8.7[-head] # security released on head
[ruby-]1.9.1[-p431]
[ruby-]1.9.2[-p330]
[ruby-]1.9.3[-p551]
[ruby-]2.0.0[-p648]
[ruby-]2.1[.10]
[ruby-]2.2[.10]
[ruby-]2.3[.8]
[ruby-]2.4[.9]
[ruby-]2.5[.7]
[ruby-]2.6[.5]
[ruby-]2.7[.0]
ruby-head

# for forks use: rvm install ruby-head-<name> --url https://github.com/github/ruby.git --branch 2.2

# JRuby
jruby-1.6[.8]
jruby-1.7[.27]
jruby-9.1[.17.0]
jruby[-9.2.11.1]
jruby-head

# Rubinius
rbx-1[.4.3]
rbx-2.3[.0]
rbx-2.4[.1]
rbx-2[.5.8]
rbx-3[.107]
rbx-4[.12]
rbx-head

# TruffleRuby
truffleruby[-20.0.0]

# Opal
opal

# Minimalistic ruby implementation - ISO 30170:2012
mruby-1.0.0
mruby-1.1.0
mruby-1.2.0
mruby-1.3.0
mruby-1[.4.1]
mruby-2.0.1
mruby-2[.1.0]
mruby[-head]

# Ruby Enterprise Edition
ree-1.8.6
ree[-1.8.7][-2012.02]

# Topaz
topaz

# MagLev
maglev-1.0.0
maglev-1.1[RC1]
maglev[-1.2Alpha4]
maglev-head

# Mac OS X Snow Leopard Or Newer
macruby-0.10
macruby-0.11
macruby[-0.12]
macruby-nightly
macruby-head

# IronRuby
ironruby[-1.1.3]
ironruby-head
[root@daluobo .ssh]# rvm install 2.6
Searching for binary rubies, this might take some time.
No binary rubies available for: centos/7/x86_64/ruby-2.6.5.
Continuing with compilation. Please read 'rvm help mount' to get more information on binary rubies.
Checking requirements for centos.
Installing requirements for centos.
Installing required packages: bison, libffi-devel, libtool.......
Requirements installation successful.
Installing Ruby from source to: /usr/local/rvm/rubies/ruby-2.6.5, this may take a while depending on your cpu(s)...
ruby-2.6.5 - #downloading ruby-2.6.5, this may take a while depending on your connection...
% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                            Dload  Upload   Total   Spent    Left  Speed
100 13.4M  100 13.4M    0     0  25063      0  0:09:23  0:09:23 --:--:-- 24933
ruby-2.6.5 - #extracting ruby-2.6.5 to /usr/local/rvm/src/ruby-2.6.5.....
ruby-2.6.5 - #configuring......................................................................
ruby-2.6.5 - #post-configuration..
ruby-2.6.5 - #compiling..^A.-

```
