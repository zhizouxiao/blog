---
layout: post
title: 向python对象动态添加方法
date: 2016-08-06
tags: 
- python
---


``` python
def barFighters( self ):
    print "barFighters"

a.barFighters = barFighters
a.barFighters()

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: barFighters() takes exactly 1 argument (0 given)

import types
a.barFighters = types.MethodType( barFighters, a )
a.barFighters()
barFighters
```
>
> 引用：
> [http://stackoverflow.com/questions/972/adding-a-method-to-an-existing-object-instance](http://stackoverflow.com/questions/972/adding-a-method-to-an-existing-object-instance)
