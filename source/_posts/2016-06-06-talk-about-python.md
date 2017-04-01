---
layout: post
title: python入门
date: 2016-06-06
tags: 
- 开发
- 语言基础
---

python是一个简单而强大的语言，应用领域非常广泛。因此，网上的优秀的入门教程非常多。
此文档只是对入门教程的补充。

<h5>python的特点</h5>
1. 拥有简单而优雅的语法，严格的格式要求, 因此代码很整洁。
2. 开源软件，经过多年的积累，拥有众多的库, 因此完全不需要重复造轮子。
3. 解释性的语言，不需要编译，能够快速执行出结果。因此，常用的调试方式，不是打断点,
而是添加日志。
4. 开发方便，不需要IDE支持，notepad也可以作为常用开发软件。
5. 网上有丰富的文档，无论你遇到神马问题，使用百度／谷歌都是很好的解决方法。

<h5>安装</h5>
1. 官方下载地址： [https://www.python.org/downloads/](https://www.python.org/downloads/)
2. 推荐版本2.7, 由于python3.x进行了语法的升级，很多库不支持3.x的语法。
3. 安装ipython，ipython是python解释器的升级版，支持语法高亮，tab补全等多个高级功能。5星推荐。
4. 安装库有两种方法, 一种是使用pip或者easy_install（命令行下安装，推荐）, 
另一种是手动下载库文件(基本上用不到)[https://pypi.python.org/pypi?%3Aaction=browse](https://pypi.python.org/pypi?%3Aaction=browse)

<h5>语法</h5>
1. 基本语法与其他语言大同小异，for循环、if条件判断、print 输出打印
2. 常用数据结构有list列表、dict字典等
3. 面向对象编程，class，支持继承

<h5>推荐教程</h5>
1. 推荐书[Dive into python](http://www.diveintopython.net/), 很薄的书，可以用来查查语法。
[中文版](http://old.sebug.net/paper/python/)
2. 推荐python 官方文档，非常丰富的文档资源[https://docs.python.org/2/](https://docs.python.org/2/)
3. 另外一个入门教程[http://www.pythondoc.com/pythontutorial27/index.html](http://www.pythondoc.com/pythontutorial27/index.html)

<h5>Hello World!</h5>
``` python
# -*- coding: utf-8 -*-
"""
auther: 一个忍不住写hello world的人。
"""
def hello():
    print "hello world!"

hello()

```
