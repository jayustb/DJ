---
title: 吴恩达神经网络DeepLearning.ai
author: DashJay
date: '2018-10-18'
slug: deeplearning-ai
categories:
  - 神经网络
tags: []
lastmod: '2018-10-18T01:28:39+08:00'
keywords: []
description: ''
comment: no
toc: no
autoCollapseToc: no
postMetaInFooter: no
hiddenFromHomePage: no
contentCopyright: no
reward: no
mathjax: no
mathjaxEnableSingleDollar: no
mathjaxEnableAutoNumber: no
hideHeaderAndFooter: no
flowchartDiagrams:
  enable: no
  options: ''
sequenceDiagrams:
  enable: no
  options: ''
---

> # 注意你可能会产生这些问题

### 1.神经网络分多少层(layers)
### 2.每层含有多少个隐藏单元(hidden units)
### 3.学习速率是多少(learning rates)
### 4.采用哪些激活函数(activation function)
- - - -

### 一.如何获得一个低误差的神经网络模型

> 不可能一开始就获得到这些数据,这是一个反复迭代的过程

你的最佳决策取决于你的数量和其他诸多因素

对于很多系统,即便是超级专家也不能配置出完美的参数,这是一个反复迭代才能达到称心如意的过程

<img src="/post/2018-10-18-deeplearning-ai_files/屏幕快照 2018-10-18 01.45.41.png" alt="" width="99%"/>

### 一.那么我们从处理偏差,方差开始解决误差的问题

> 过度拟合和欠拟合都是一种常见的问题
<img src="/post/2018-10-18-deeplearning-ai_files/屏幕快照 2018-10-18 01.49.04.png" alt="" width="99%"/>

图左是欠拟合,认为不够精细无法区分样本

图右是过拟合,可能只试用与该样本,而无法满足任何变化

中间的是合理拟合度

> 最优误差被称作贝叶斯误差:很低

> 高偏差和高方差
<img src="/post/2018-10-18-deeplearning-ai_files/屏幕快照 2018-10-18 01.58.01.png" alt="" width="99%"/>

### 二.当误差过大甚至无法拟合的时候:

换一个模型,选择一个新的网络来进行训练,可能有用也可能没用,你必须去尝试一下.

只要人能分辨,网络够大,也就能分辨出来,至少可以很好拟合出来

高偏差其实准备更多数据也没用,但是高偏差和高方差不是同一件事 


### 三.什么是正则化

>如果你怀疑你的神经网络过度拟合(overfitting)了数据,方差过高,最先想到的就应该是正则化sssss然后其次就是准备更多的数据

正则化可以避免过度拟合 

L2正则化,的数学公式完全没有看懂没有听懂.作为一个必须立即的内容留下来