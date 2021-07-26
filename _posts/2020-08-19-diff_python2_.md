---
layout: article                       # 不变
title:  "Differences between Python 2 and Python 3"     # 文章标题
date:   2020-08-19 17:34:40 +0800     # 编写时间，不要超过当前系统时间，否则编译不通过
key:  diff_python_23               # 文章的唯一 ID，不要重复了
aside:
  toc: true
category: [python, blog]                # 重点来了，这是类别标签（什么名字都可以，别和其他标签重了）
sidebar:
    nav: Blog
---
## division ##
* Python 2 (By default integer division)

```
assert 1 / 2 == 0
```
* Python 3 (By default true division)

```
assert 1 / 2 == 0.5
```
* Remedy for Python 2 (forward compatible to Python 3)
  
```
from __future__ import division
```

## print ##
* Python 2 (no parentheses)
```
print 'I am a print function'
```
* Python 3

```
print('I am a print function')

```
* Remedy
```
from __future__ import print_function
```

## range and xrange ##
* Python 2 (```xrange``` runs identity check)

```
assert xrange(5) != xrange(5)
```
* Python3 (```range``` runs equality check)

```
assert range(5) == range(5)
```

## input and raw_input ##

* Python 2 (```input()``` depends on input type)
   
```
a = input('a') # ->> 123
print type(a) # <type 'int'>

a = input('a') # ->> '123'
print type(a) # <type 'str'>
```

* Python 2 (```raw_input()```) and Python 3 (```input()```)  
Always return ```str``` output.