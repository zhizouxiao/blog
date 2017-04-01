---
layout: post
title: (linux网络)netstat
date: 2016-12-16
tags: 
- linux网络
---

#### netstat
netstat 用于列出所有tcp，udp连接

1. 显示当前所有活动的网络连接  
    ~ » netstat -an | head -n 10                                                    wazi@eli
    Active Internet connections (including servers)
    Proto Recv-Q Send-Q  Local Address          Foreign Address        (state)  
    tcp4       0      0  172.16.13.172.54304    180.149.131.55.8843    SYN_SENT  
    tcp4       0      0  172.16.13.172.54303    45.32.41.155.44005     ESTABLISHED  
    tcp4       0      0  127.0.0.1.60409        127.0.0.1.54302        ESTABLISHED  
    tcp4       0      0  127.0.0.1.54302        127.0.0.1.60409        ESTABLISHED  
    tcp4       0      0  172.16.13.172.54300    45.32.41.155.44005     ESTABLISHED  
    tcp4       0      0  127.0.0.1.60409        127.0.0.1.54299        ESTABLISHED  
    tcp4       0      0  127.0.0.1.54299        127.0.0.1.60409        ESTABLISHED  
    tcp4       0      0  172.16.13.172.54296    111.203.187.167.3306   ESTABLISHED  

    连接状态：  
    LISTEN：侦听来自远方的TCP端口的连接请求  
    SYN-SENT：再发送连接请求后等待匹配的连接请求  
    SYN-RECEIVED：再收到和发送一个连接请求后等待对方对连接请求的确认  
    ESTABLISHED：代表一个打开的连接  
    FIN-WAIT-1：等待远程TCP连接中断请求，或先前的连接中断请求的确认  
    FIN-WAIT-2：从远程TCP等待连接中断请求  
    CLOSE-WAIT：等待从本地用户发来的连接中断请求    
    CLOSING：等待远程TCP对连接中断的确认  
    LAST-ACK：等待原来的发向远程TCP的连接中断请求的确认  
    TIME-WAIT：等待足够的时间以确保远程TCP接收到连接中断请求的确认  
    CLOSED：没有任何连接状态  

2. 显示所有连接ip
netstat -n -p | grep ES | awk '{print $5}' | awk -F: '{print $1}'

3. 显示数量
netstat -anp |grep 'tcp|udp' | awk '{print $5}' | cut -d: -f1 | sort | uniq -d
