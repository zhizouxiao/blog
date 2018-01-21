---
title: Mac相关
date: 2017-04-29 22:54:14
tags: Mac
---

### Mac相关

``` shell
# mac启动ftp服务器
sudo -s launchctl load -w /System/Library/LaunchDaemons/ftp.plist

# mac检查占用80端口的进程
sudo lsof -n -i:80 | grep LISTEN
```
