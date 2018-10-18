---
title: 密码学Information security
author: Dashjay
date: '2018-10-15'
slug: information-security
categories:
  - 密码学
tags:
  - RSA
lastmod: '2018-10-15T10:50:31+08:00'
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

# 我看的视频如下
{{% youtube "D_kMadCtKp8" %}}

然后以下是笔记

### 1.对称加密

> A m-(+e)->C

> B m-(-e)<-C

对称解码

### 2.非对称加密

<img src="/post/2018-10-15-information-security_files/屏幕快照 2018-10-15 10.58.40.png" alt="" width="99%"/>

- - - -
### RSA加密算法基本原理

1. 找出两个质数p,q
2. n = p*q
3. $ \phi(n) = (p-1)(q-1) $ 欧拉函数
4.公钥 e (1 < e < $\phi n$)
e 和 $ \phi(n)$ 互质
生成私钥d,ed除$ \phi(n)$ 余数为1

5.加密 ,想传数字m,  $m^e$除n求余数c
6.解密数字$c^d$ ,除n求余数 一定是m

