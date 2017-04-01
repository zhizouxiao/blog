---
layout: post
title: game robot
date: 2015-06-30
tags: 
- 开发
- 工具
- 项目
---

load test for game server. [source code](https://github.com/zhizouxiao/game-robot.git) has been hosted on Github. 


<h3>Main features</h3>
1. client basic feature: connect, logic injection
2. client manager, multi client
3. statistics


<h3>Process</h3>
first, fork the [boom](https://github.com/tarekziade/boom).


then, modify the code for game server test.  

1. add the client with raw socket;
2. add base features for game server:register/login;
3. add logic injection;
