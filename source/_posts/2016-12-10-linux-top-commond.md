---
layout: post
title: (linux常用命令)top
date: 2016-12-10
tags: 
- linux
---

##### top 命令
``` bash

top -c
top - 17:48:50 up 151 days,  3:31,  1 user,  load average: 0.07, 0.12, 0.09
Tasks: 132 total,   1 running, 131 sleeping,   0 stopped,   0 zombie
Cpu(s):  1.0%us,  0.5%sy,  0.2%ni, 98.3%id,  0.0%wa,  0.0%hi,  0.0%si,  0.0%st
Mem:   4194304k total,  4179548k used,    14756k free,        0k buffers
Swap:  2097152k total,   782360k used,  1314792k free,  1977088k cached

PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND
1033 mysql     20   0 1158m 7988 1620 S  0.3  0.2  30:16.67 /usr/libexec/mysqld --basedi
7134 tyhall    20   0 1605m 167m  15m S  0.3  4.1   0:29.42 pypy run.py UT001 192.168.10
7136 tyhall    20   0  347m 166m  17m S  0.3  4.1   0:24.37 pypy run.py GT21-001-998-1 1

17:48:50 ： 系统当前时间
151 days, 3:31 ： 系统开机到现在经过了多少时间
1 users ： 当前2用户在线
load average: 0.07, 0.12, 0.09： 系统1分钟、5分钟、15分钟的CPU负载信息

Tasks：任务;
132 total：当前有132个进程。
1 running：1个进程正在运行
131 sleeping：131个进程睡眠
0 stopped：停止的进程数
0 zombie：僵死的进程数

Cpu(s)：表示这一行显示CPU总体信息
1.0%us：用户态进程占用CPU时间百分比，不包含renice值为负的任务占用的CPU的时间。
0.5%sy：内核占用CPU时间百分比
0.2%ni：改变过优先级的进程占用CPU的百分比
98.3%id：空闲CPU时间百分比
0.0%wa：等待I/O的CPU时间百分比
0.0%hi：CPU硬中断时间百分比
0.0%si：CPU软中断时间百分比
注：这里显示数据是所有cpu的平均值，如果想看每一个cpu的处理情况，按1即可；折叠，再次按1；(centos)

Mem：内存
4194304k total：物理内存总量
4179548k used：使用的物理内存量
14756k free：空闲的物理内存量
0k buffers：用作内核缓存的物理内存量

Swap：交换空间
2097152k total：交换区总量
782360k used：使用的交换区量
1314792k free：空闲的交换区量
1977088k cached：缓冲交换区总量

PID：进程的ID
USER：进程所有者
PR：进程的优先级别，越小越优先被执行
NI：值Nice Value 如果为负值，则有较高优先级；如果为正值则为较低优先级；如果为0，则无优先级调整
VIRT：进程占用的虚拟内存
RES：进程占用的物理内存
SHR：进程使用的共享内存
S：进程的状态。S表示休眠，R表示正在运行，Z表示僵死状态，N表示该进程优先值为负数
%CPU：进程占用CPU的使用率
%MEM：进程使用的物理内存和总内存的百分比
TIME+：该进程启动后占用的总的CPU时间，即占用CPU使用时间的累加值。
COMMAND：进程启动命令名称

q：退出top命令
<Space>：立即刷新
s：设置刷新时间间隔
c：显示命令完全模式
t: 显示或隐藏进程和CPU状态信息
m：显示或隐藏内存状态信息
l：显示或隐藏uptime信息
f：增加或减少进程显示标志
S：累计模式，会把已完成或退出的子进程占用的CPU时间累计到父进程的MITE+
P：按%CPU使用率排行
T：按MITE+排行
M：按%MEM排行
u：指定显示用户进程
r：修改进程renice值
k: kill进程
i：只显示正在运行的进程
W：保存对top的设置到文件^/.toprc，下次启动将自动调用toprc文件的设置。
h：帮助命令。
q：退出

如果只需要查看内存：可用free命令。只查看uptime信息（第一行），可用uptime命令；
```
