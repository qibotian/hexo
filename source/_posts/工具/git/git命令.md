---
title: git命令
id: gitCommand
date: 2019-08-23
categories: ['工具']
tags: ['git','branch']
comments: true
---

[tob]

# 1. 远程仓库操作

1）检出仓库

```bash
$ git clone git://github.com/xxx/xxxx.git
```
2）查看远程仓库
```bash
$ git remote -v
```

3）添加远程仓库
```bash
$ git remote add [name] [url]
```

4）删除远程仓库
```bash
$ git remote rm [name]
```

5）修改远程仓库
```bash
$ git remote set-url --push[name][newUrl]
```
6）拉取远程仓库
```bash
$ git pull [remoteName] [localBranchName]
```

7）推送远程仓库
```bash
$ git push [remoteName] [localBranchName]
```

# 2. 分支操作命令
1) 查看本地分支
```bash
$ git branch
```
2) 查看远程分支
```bash
$ git branch -r
```
3) 创建本地分支
```bash
$ git branch [name] ----注意新分支创建后不会自动切换为当前分支
```
4) 切换分支
```bash
$ git checkout [name]
```

5) 创建分支并切换分支
```bash
$ git checkout -b [name]
```

6) 删除分支
```bash
$ git branch -d [name] ---- -d选项只能删除已经参与了合并的分支，对于未有合并的分支是无法删除的。如果想强制删除一个分支，可以使用-D选项
```

7) 删除分支
```bash
$ git merge [name] ----将名称为[name]的分支与当前分支合并
```

8) 创建远程分支(本地分支push到远程
```bash
$ git push origin [name]
```

9) 删除远程分支(本地分支push到远程
```bash
$ git push origin :heads/[name]
```

# 3. TAG操作命令
1) 查看版本
```bash
$ git tag
```

2) 创建版本
```bash
$ git tag [name]
```

3) 删除版本
```bash
$ git tag -d [name]
```

4) 查看远程版本
```bash
$ git tag -r
```

5) 创建远程版本(本地版本push到远程)
```bash
$ git push origin [name]
```

6) 删除远程版本
```bash
$ git push origin :refs/tags/[name]
```
