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

#### 去重复uniq
``` bash
# uniq
# 121.43.187.116:8000
# 121.43.187.116:8000
# 121.43.187.116:8000
cut -d : -f 1 | uniq
```

#### cut
``` bash
主要参数
-b ：以字节为单位进行分割。这些字节位置将忽略多字节字符边界，除非也指定了 -n 标志。
-c ：以字符为单位进行分割。
-d ：自定义分隔符，默认为制表符。
-f  ：与-d一起使用，指定显示哪个区域。
-n ：取消分割多字节字符。仅和 -b 标志一起使用。如果字符的最后一个字节落在由 -b 标志的 List 参数指示的<br />范围之内，该字符将被写出；否则，该字符将被排除。
```


