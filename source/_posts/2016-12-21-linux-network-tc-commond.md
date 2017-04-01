---
layout: post
title: (linux网络)tc
date: 2016-12-21
tags: 
- linux网络
---

#### tc
tc 网络状况
1. 增加延迟100ms ± 10ms  
tc qdisc change dev eth0 root netem delay 100ms 10ms  

2. 增加延迟100ms  ± 10ms, 下一个随机数25%依赖于上一个
tc qdisc change dev eth0 root netem delay 100ms 10ms 25%

3. 随机丢包0.1%
tc qdisc change dev eth0 root netem loss 0.1%

