---
layout: article                       # 不变
title:  "(TensorBoard) Non-refreshing TensorBoard"     # 文章标题
date:   2020-12-27 17:34:40 +0800     # 编写时间，不要超过当前系统时间，否则编译不通过
key:   tensorboard               # 文章的唯一 ID，不要重复了
aside:
  toc: true
category: [MLF, blog]                # 重点来了，这是类别标签（什么名字都可以，别和其他标签重了）
sidebar:
    nav: Blog
---
After the operations like ```writer.add_scalar()```, please don't forget to use ```writer.flush()``` to write the buffer to the file.