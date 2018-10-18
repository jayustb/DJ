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