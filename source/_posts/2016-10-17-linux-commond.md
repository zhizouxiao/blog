---
layout: post
title: linux常用命令
date: 2016-10-17
tags: 
- linux
---


##### 文件操作
``` bash
# 拆分文件 split
split -l 100 myfile prefix #按行拆分
split -b 100k myfile prefix #按大小拆分
```

##### 文件浏览

``` bash
# 倒序输出 tac
tac myfile
```

##### tar压缩与解压缩

``` bash
#  .tar
tar -cvf tecmint-14-09-12.tar /home/tecmint/
tar -xvf tecmint-14-09-12.tar /home/tecmint/
# .tar.gz
tar cvzf MyImages-14-09-12.tar.gz /home/MyImages
tar xvzf MyImages-14-09-12.tar.gz /home/MyImages
# .tar.bz2
tar cvjf MyImages-14-09-12.tar.gz /home/MyImages
tar xvjf MyImages-14-09-12.tar.gz /home/MyImages
```

#### 查找不包含的文件
``` bash
find . ! -name "*.2017_04_24" -type f
```

#### docker attach第一个container
``` bash
sudo docker attach `sudo docker ps |grep "day" | cut -d" " -f1`
```

