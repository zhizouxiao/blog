---
layout: post
title: 查看磁盘使用
date: 2016-06-07
tags: 
- linux
---
### centos 查看磁盘空间利用大小:
df -h

### 查看当前目录所占空间大小:
du -sh

### du命令查看一级目录

centos: du -h --max-depth=1  
![mac]({{ site.baseurl }}/public/post/du_centos.gif)

mac: du -hd1\n
![mac]({{ site.baseurl }}/public/post/du_mac.gif)
