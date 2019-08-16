---
title: git每次push.pull都提示Enter passphrase for key 'sshid_rsa_github'.md
date: 2019-08-14
categories: ['工具']
tags: ['git','passphrase']
comments: true
---

git每次push.pull都提示Enter passphrase for key 'sshid_rsa_github'

<!--more-->

git每次push.pull都提示Enter passphrase for key 'sshid_rsa_github'， 这是要输入当时创建key的密码。  
有两种方式可以解决：  
 * 创新生成一个key  
 * 将密钥假如到ssh-agent的高速缓存中

这里主要介绍第二种方法：

  ```
    //这里假设提示：Enter passphrase for key '/c/.ssh/id_rsa_github_XXXXX':

    //输入以下命令（不带前面的#号）
    # ssh-add -k /c/.ssh/id_rsa_github_XXXXX

    //如果此时提示：Could not open a connection to your authentication agent.
    //继续输入
    # ssh-agent bash

    //重新输入
    # ssh-add -k /c/.ssh/id_rsa_github_XXXXX

    //此时会提示 Enter passphrase for /c/.ssh/id_rsa_github_XXXXX:
    //我们在输入自己的密码后，如果成功则会提示： Identity added: /c/.ssh/id_rsa_github_XXXXX (/c/.ssh/id_rsa_github_XXXXX)
    //此时大功告成了

  ```
