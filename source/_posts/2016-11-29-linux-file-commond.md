---
layout: post
title: (linux常用命令)文件与目录
date: 2016-11-29
tags: 
- linux
---

##### 文件操作
``` bash

# 查看当前目录下文件个数
find ./ | wc -l

# 查找目标文件夹中是否有obj文件:

$find ./ -name '*.o'

# 查找并删除.svn
find . -name ".svn" | xargs rm -Rf

# ls按照时间排序
ls -lrt

# 拆分文件 split
split -l 100 myfile prefix #按行拆分
split -b 100k myfile prefix #按大小拆分

##### 文件浏览

# 倒序输出 tac
tac myfile

# 显示文件前几行
head -10 filename

# 显示文件后几行
tail -10 filename


#### 文件与目录权限
# 改变文件的拥有者
chown user:user file

# 递归子目录修改 
chown -R user source/

# 改变文件读，写，执行等属性
chmod 600 id_rsa

# 增加脚本可执行权限
chmod a+x myscript



##### tar压缩与解压缩

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
