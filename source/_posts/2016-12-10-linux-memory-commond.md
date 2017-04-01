---
layout: post
title: (linux常用命令)内存
date: 2016-12-10
tags: 
- linux
---

##### free 命令
``` bash

free -h 
             total       used       free     shared    buffers     cached
Mem:          4.0G       2.6G       1.4G       5.0M         0B       426M
-/+ buffers/cache:       2.2G       1.8G
Swap:         2.0G       766M       1.3G

buffer：将要写到磁盘上的内容
cached: 缓存到内存，供以后使用的数据
2.2G: used(2.6G) - buffer(0B) - cached(426M) 
1.8G: used(1.4G) + buffer(0B) + cached(426M) 

```


#### vmstat 命令
``` bash
shell: vmstat -S m  1 3
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 2  0      0    314    323  14996    0    0     1    25    1    5  1  1 98  0  0
 0  0      0    314    323  14996    0    0     0   164 1236 2243  3  1 95  1  0
 0  0      0    312    323  14996    0    0     0    72 1233 2324  3  1 95  0  0

Procs（进程）:
r: 运行队列中进程数量
b: 等待IO的进程数量

Memory（内存）:
swpd: 使用虚拟内存大小
free: 可用内存大小
buff: 用作缓冲的内存大小
cache: 用作缓存的内存大小

Swap:
si: 每秒从交换区写到内存的大小
so: 每秒写入交换区的内存大小

IO：（现在的Linux版本块的大小为1024bytes）
bi: 每秒读取的块数
bo: 每秒写入的块数

system：
in: 每秒中断数，包括时钟中断
cs: 每秒上下文切换数

CPU（以百分比表示）
us: 用户进程执行时间(user time)
sy: 系统进程执行时间(system time)
id: 空闲时间(包括IO等待时间)
wa: 等待IO时间

```
