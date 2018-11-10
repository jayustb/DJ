---
title: 又得重新学习TensorFlow
author: DashJay
date: '2018-10-17'
slug: tensorflow
categories:
  - TensorFlow
tags:
  - 人工智能
lastmod: '2018-10-17T01:16:36+08:00'
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

>坑爹搭建环境用了我很长时间啊

## 1.首先我安装了Anaconda创建了一个一个环境叫做`TensorFlow`

## 2.`conda create -n tensorflow`创建了这个环境
>中间省略了一大堆坑,各种C++库链接不上,各种问题,最后解决了

## 3. 安装了`TensorFlow,skimage`等库然后开始尝试读取图片内容了

由于一张大图比较复杂所以我导入的大图看不出规律,因此我导入了一张`2x2`的图片,4个像素

<img src="/post/2018-10-17-tensorflow_files/屏幕快照 2018-10-17 23.32.12.png" alt="" width="99%"/>

>从左上角开始向右上角读图片,储存成数组的第一维度,每个维度由四个数值组成,分别是RGBA.
- - - -
> img = [[第一行],[第二行]]
- - - -
> 第一行 = [[R,G,B,A],.......,[R,G,B,A]]
- - - - 
每一个[RGBA]代表一个像素点

``` python
img = 
[
[[R,G,B,A],......,[R,G,B,A]] # 第一行
[[R,G,B,A],......,[R,G,B,A]] # 第二行
......
[[R,G,B,A],......,[R,G,B,A]] # 第n行
# 每个[R,G,B,A]就是一个像素点
]

```


该2x2图片里储存的,信息就如下


<img src="/post/2018-10-17-tensorflow_files/屏幕快照 2018-10-17 23.36.45.png" alt="" width="90%"/>


<center><img src="/post/2018-10-17-tensorflow_files/dddpng" alt="" width="40%"/></center>

拿到像素点的信息之后我们就可以干活了,比如我们通过数学公式来判断,图像里面的信息,内容

> 我想到一个案例

## 然后我就开始在网易云课堂上开始学习申请经网路了
