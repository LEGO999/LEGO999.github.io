---
layout: article                       # 不变
title:  "Strategies for Imbalanced Data"     # 文章标题
date:   2020-10-07 17:34:40 +0800     # 编写时间，不要超过当前系统时间，否则编译不通过
key:   strategies_for_imbalance               # 文章的唯一 ID，不要重复了
aside:
  toc: true
category: [ML, blog]                # 重点来了，这是类别标签（什么名字都可以，别和其他标签重了）
sidebar:
    nav: Blog
---
Addressing issues of data imbalanced has many strategies. Another keyword: long-tailed distribution.
1. (Easiest) Oversamping and downsampling  
   * Cons of oversampling: overfitting  
   * Cons of downsampling: wasting data  
2. (Binary classification) Adjustment of prediction threshold  
   If the ratio is 3:7, the classification probability threshold should be adjusted to 0.3 from 0.5.
3. (Common) Loss weight adjustment  
   The loss weight should be inversely proportional to the data ratio. If the ratio is 3:7 in binary classification, the weight should be 7:3.
4. (For non-severe imbalance) Ensemble and K-fold split  
   If the ratio is 1:9 in binary classification, samples in the major class are split into 9 subsets. The minor class remains the same. Eventually, each subset will have balanced data ratio of 1:1. Each subset will be assigned a classifier. The final output is provided by the ensemble of the all 9 sub-classifiers.
5. (Hard/easy samples imbalance) OHEM ([Online Hard Examples Mining](https://arxiv.org/pdf/1604.03540.pdf)) or [focal loss](https://arxiv.org/abs/1708.02002)  
6. [Decoupling](https://openreview.net/pdf?id=r1gRTCVFvB)  
   Train a CNN+FC normal classifier with imbalanced data. Fix the classifier and add an additional FC layer after it. Train the whole DNN with balanced data.

