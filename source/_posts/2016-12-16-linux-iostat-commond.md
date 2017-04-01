---
categories: tech
layout: post
title: (linux常用命令)iostat
date: 2016-12-16
tags: 
- linux
---

#### CPU  

iostat  
avg-cpu:  %user   %nice %system %iowait  %steal   %idle  
          1.95    0.06    0.41    0.03    0.00   97.56  
cpu属性值说明：  
%user：CPU处在用户模式下的时间百分比。  
%nice：CPU处在带NICE值的用户模式下的时间百分比。  
%system：CPU处在系统模式下的时间百分比。  
%iowait：CPU等待输入输出完成时间的百分比。  
%steal：管理程序维护另一个虚拟处理器时，虚拟CPU的无意识等待时间百分比。  
%idle：CPU空闲时间百分比。  

注：  
1. 如果%iowait的值过高，表示硬盘存在 I/O瓶颈，  
2. %idle值高，表示CPU较空闲，如果%idle值高但系统响应慢时，有可能是CPU等待分配内存， 
此时应加大内存容量。  
3. %idle值如果持续低于10，那么系统的CPU处理能力相对较低，表明系统中最需要解决的资源是CPU。 

#### Disk  

iostat -d -x -k 1 1  

Device:         rrqm/s   wrqm/s     r/s     w/s    rkB/s    wkB/s avgrq-sz avgqu-sz   await r_await w_await  svctm  %util  
vda               0.00     7.38    0.04    4.60     0.73    63.26    27.59     0.06   12.58   19.94   12.53   6.63   3.07  
vdb               0.00     6.97    0.21    6.14     6.30   180.95    58.99     0.07   11.59    4.15   11.85   0.61   0.39  
rrqm/s: 每秒进行 merge 的读操作数目。即 rmerge/s  
wrqm/s: 每秒进行 merge 的写操作数目。即 wmerge/s  
r/s: 每秒完成的读 I/O 设备次数。即 rio/s  
w/s: 每秒完成的写 I/O 设备次数。即 wio/s  
rsec/s: 每秒读扇区数。即 rsect/s  
wsec/s: 每秒写扇区数。即 wsect/s  
rkB/s: 每秒读K字节数。是 rsect/s 的一半，因为每扇区大小为512字节。  
wkB/s: 每秒写K字节数。是 wsect/s 的一半。  
avgrq-sz: 平均每次设备I/O操作的数据大小 (扇区)。  
avgqu-sz: 平均I/O队列长度。  
await: 平均每次设备I/O操作的等待时间 (毫秒)。  
svctm: 平均每次设备I/O操作的服务时间 (毫秒)。  
%util: 一秒中有百分之多少的时间用于 I/O 操作，即被io消耗的cpu百分比  

备注：如果 %util 接近 100%，说明产生的I/O请求太多，I/O系统已经满负荷，该磁盘可能存在瓶颈。
如果 svctm 比较接近 await，说明 I/O 几乎没有等待时间；如果 await 远大于 svctm，说明I/O 队列太长，
io响应太慢，则需要进行必要优化。如果avgqu-sz比较大，也表示有当量io在等待。
如果 %util 接近 100%，说明产生的I/O请求太多，I/O系统已经满负荷，该磁盘可能存在瓶颈。 idle小于70% IO压力就较大了，一般读取速度有较多的wait。 同时可以结合vmstat 查看查看b参数(等待资源的进程数)和wa参数(IO等待所占用的CPU时间的百分比，高过30%时IO压力高)。

另外 await 的参数也要多和 svctm 来参考。差的过高就一定有 IO 的问题。

avgqu-sz 也是个做 IO 调优时需要注意的地方，这个就是直接每次操作的数据的大小，如果次数多，但数据拿的小的话，其实 IO 也会很小。如果数据拿的大，才IO 的数据会高。也可以通过 avgqu-sz × ( r/s or w/s ) = rsec/s or wsec/s。也就是讲，读定速度是这个来决定的。

svctm 一般要小于 await (因为同时等待的请求的等待时间被重复计算了)，svctm 的大小一般和磁盘性能有关，CPU/内存的负荷也会对其有影响，请求过多也会间接导致 svctm 的增加。await 的大小一般取决于服务时间(svctm) 以及 I/O 队列的长度和 I/O 请求的发出模式。如果 svctm 比较接近 await，说明 I/O 几乎没有等待时间；如果 await 远大于 svctm，说明 I/O 队列太长，应用得到的响应时间变慢，如果响应时间超过了用户可以容许的范围，这时可以考虑更换更快的磁盘，调整内核 elevator 算法，优化应用，或者升级 CPU。

队列长度(avgqu-sz)也可作为衡量系统 I/O 负荷的指标，但由于 avgqu-sz 是按照单位时间的平均值，所以不能反映瞬间的 I/O 洪水。

形象的比喻：
r/s+w/s 类似于交款人的总数
平均队列长度(avgqu-sz)类似于单位时间里平均排队人的个数
平均服务时间(svctm)类似于收银员的收款速度
平均等待时间(await)类似于平均每人的等待时间
平均I/O数据(avgrq-sz)类似于平均每人所买的东西多少
I/O 操作率 (%util)类似于收款台前有人排队的时间比例
设备IO操作:总IO(io)/s = r/s(读) +w/s(写)

平均等待时间=单个I/O服务器时间*(1+2+...+请求总数-1)/请求总数

每秒发出的I/0请求很多,但是平均队列就4,表示这些请求比较均匀,大部分处理还是比较及时。


