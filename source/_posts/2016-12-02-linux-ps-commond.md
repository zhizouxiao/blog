---
layout: post
title: (linux常用命令)进程
date: 2016-12-02
tags: 
- linux
---

##### ps 命令
``` bash

# 显示所有进程
ps -ef
ps aux
#u,f 表示显示详细信息

#显示某用户进程 -u
ps -f -u username

#根据进程id显示进程信息
ps -f  -p 3150,7298,6544

# 显示树型进程, --forest
ps -f --forest -C pypy

# -C 进程名称

# 显示子进程
ps -o pid,uname,comm -C apache2
#选择显示列 -o

```

