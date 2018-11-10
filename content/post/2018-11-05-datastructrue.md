---
title: 总结鹏哥的一席话DataStructrue
author: Dashjay
date: '2018-11-05'
slug: datastructrue
categories:
  - 数据结构
tags:
  - 算法
lastmod: '2018-11-05T00:02:54+08:00'
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

<!--more-->
> #新来806,听鹏哥做了五六年游戏,谈了几句,鹏哥给我讲了很多内容,由于时间原因只能稍作记录未来再补全

## 字典树[hashfunc]

> 字典是一种无序的结构,常常可以在O(1)的时间内增删查改,非常方便

`public Dictionary<string,T> dic;`

`public Dictionary<int,T> dic2;`

以上两种字典都是我们在C#中常用的字典,但是我们没有想过为什么它本身是无序的,需要增删查改的时候却只有O(1)的复杂度.

这是字典树的功劳,也是hashfunc的功劳.

当我们尝试储存很多键值对的时候,往往是键的输入转化成了一个不唯一的hash数值,让他对应到一个字典hash表中的一列

假如我向字典中添加进了`'abc': Hero`这组数据,那么计算机会把`'abc'`通过`hashfunc()`转化成一个对应的hash数值,并且找到目标位置放入
假如hash数值是621那么
<center><img src="/post/2018-11-05-datastructrue_files/屏幕快照 2018-11-05 00.42.32.png" alt="" width="99%"/></center>

当我们想要找这个数值的时候再同伙hash算法返回找到那个对应的键值对并且返回,这是非常快速的,但是有时候会出现一个可能是偶然出现的问题,就是两个键会对应同一个hash数值

例如

> hashfunc('abc') = 621

> hashfunc('acd') = 621


这时候hash数值就有点不管用了,要上hash树,hash树的原理其实很简单就是,生成一个不够我生成两个,两个不够我生成三个,反正就是能匹配上.

<img src="/post/2018-11-05-datastructrue_files/屏幕快照 2018-11-05 00.50.53.png" alt="" width="99%"/>

总之以上内容很简单但是比较冷门
今天先总结那么多,其他的明天再说 2018年11月5日周一00:56
- - - -