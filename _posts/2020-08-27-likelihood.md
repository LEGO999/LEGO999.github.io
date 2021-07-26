---
layout: article                       # 不变
title:  "Difference between Likelihood, Negative Log-likelihood, Entropy, Cross-entropy and KL Divergence"     # 文章标题
date:   2020-08-27 17:34:40 +0800     # 编写时间，不要超过当前系统时间，否则编译不通过
key:   Likelihood               # 文章的唯一 ID，不要重复了
aside:
  toc: true
category: [ML, blog]                # 重点来了，这是类别标签（什么名字都可以，别和其他标签重了）
sidebar:
    nav: Blog
---

## Likelihood ##
Assume a three-class classification problem with one-hot coding label $y_i$. The observation (output of DNNs) of a sample is $\hat{y}_i$.  
The equation $$\text{Likelihood} = \sum_{0}^{i}\hat{y}_i^{y_i}$$ computes the likelihood of the sample.

| Object | $\hat{y}_i$|$y_i$|
| --| --|--|
|Cat|0.7|1|
|Dog|0.2|0|
|Car|0.1|0|

So the likelihood is $$Likelihood = 0.7^1 + 0.2^0 + 0.1^0 = 0.7$$. DNNs maximize the likelihood estimation.
## Negative Log-Likelihood (NLL) ##
In convex optimization, optimizers tend to use the concept of reduction rather than incrementation. So maximizing likelihood is equivalent to minimize negative likelihood. Additionally, adding a logarithmic function(convex function) could transform exponentiation to multiplication. This transformation also renders final loss function positive. That where the term negative log-likelihood (NLL) comes from.  
$$\text{NLL} = -\sum_{0}^{i}y_i \log \hat{y_i}$$  
Following the previous example, $$\text{NLL}=-1\times \log 0.7 = 0.3567$$

## Entropy ##
Assume that we have a discrete random variable $x$ with probability mass function (PMF) $\mathbf{f}(x)$. Entropy measures the uncertainty of $x$. In other words, how peaky is the distribution of $\mathbf{f}(x)$. The larger is the entropy, the more uncertain is the variable $x$.  
$$\text{Entropy} = -\sum \mathbf{f}(x) \log \mathbf{f}(x)$$  
Following the previous example, $$\text{Entropy} = -\left(0.7\times\log 0.7 + 0.2\times\log 0.2 + 0.1\times\log 0.1\right) = 0.9087$$
## Cross-entropy ##
Cross-entropy isn't entropy. Cross-entropy links another distribution $\mathbf{g}(x)$ to $\mathbf{f}(x)$, replacing one of the $\mathbf{f}(x)$ in the entropy interpretations.  
$$\text{Cross-entropy} = -\sum \mathbf{g}(x) \log \mathbf{f}(x)$$  
In the context of DNNs, cross-entropy is equal to negative log-likelihood. $\mathbf{g}(x)$ could be interpreted as labels and $\mathbf{f}(x)$ could be interpreted as predictions.

## KL Divergence ##
Kullback-Leibler Divergence (KL divergence) measures the distance between two distributions. 
$$D_{KL} = \sum \mathbf{g}(x) \log\frac{\mathbf{g}(x)}{\mathbf{f}(x)}$$  
where $\mathbf{f}(x)$ and $\mathbf{g}(x)$ are two different distributions.
Rewrite KL divergence in the following form:  
$$D_{KL} = \underbrace{-\sum \mathbf{g}(x)\log\mathbf{f}(x)}_{\text{cross-entropy between }\mathbf{g(x)} \text{ and } \mathbf{f(x)}}-\underbrace{-\sum\mathbf{g}(x)\log\mathbf{g}(x)}_{\text{Entropy of } \mathbf{g(x)}}$$  
Since the entropy of $\mathbf{g}(x)$ is a fixed term and not related to $\mathbf{f}(x)$, it will be neglected in the optimization. Therefore, to optimize KL divergence is equivalent to optimize cross-entropy.  
For one-hot coding labels, only the target probability is concerned. Cross-entropy equals logarithmic probability of target and could save some computation.  
However, if soft labels are applicable, KL divergence should be used rather than cross-entropy for the following reasons:
* Cross-entropy doesn't save computation since all probabilities should be enumerated.
* Cross-entropy doesn't indicate zero gradient properly. A zero gradient example is shown as follows: 
    *  predictions: $\begin{bmatrix}0.95 &0.05\end{bmatrix}$
    *  labels: $\begin{bmatrix}0.95 &0.05\end{bmatrix}$
    *  $D_{KL} = 0.95\times \log\frac{0.95}{0.95} + 0.05\times \log\frac{0.05}{0.05} = 0$
    *  $\text{Cross-entropy} = -(0.95\times\log0.95 + 0.05\times\log0.05)= 0.1985$

## Reference ##
 1. [glassbox](https://glassboxmedicine.com/2019/12/07/connections-log-likelihood-cross-entropy-kl-divergence-logistic-regression-and-neural-networks/)