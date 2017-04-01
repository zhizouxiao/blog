---
layout: post
title: svn常用命令
date: 2016-07-25
tags: 
- 工具
comments: true
---


1. 显示前10条log  
``` bash
svn log -l 10
```

2. 显示版本差异,只输出文件名  
``` bash
svn diff --summarize  -r954:958
```

3. 回退到历史版本
``` bash
svn merge -r 958:954 ""
svn diff
svn commit -m "revert"
```
