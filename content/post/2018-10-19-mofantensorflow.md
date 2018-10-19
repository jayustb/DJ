---
title: TensorFlow莫凡
author: DashJay
date: '2018-10-19'
slug: mofantensorflow
categories:
  - TensorFlow
tags:
  - 人工智能
lastmod: '2018-10-19T23:04:28+08:00'
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


> # 这个项目之前已经做了好多次了,今天纯手打了一次

```python

import tensorflow as tf
import numpy as np

# create data
x_data=np.random.rand(100).astype(np.float32)
y_data=x_data*0.1+0.3

## create tensorflow structure start ##

# 用随机的方式生成的随机数列,1代表一维结构(-1,1)
Weights = tf.Variable(tf.random_uniform([1],-1.0,1.0))

# 1代表一维结构(初始值是0)
biases=tf.Variable(tf.zeros([1]))

# 预测值
y = Weights*x_data+biases

# 计算差别
loss = tf.reduce_mean(tf.square(y-y_data))

# 选择最基础的优化器 ，学习效率设置为0.5
opt = tf.train.GradientDescentOptimizer(0.5)

# 求最小值吧也许
train = opt.minimize(loss)

# 初始化所有数值
init = tf.initialize_all_variables()

## create tensorflow structure end ##


# 神经网络Session
sess = tf.Session()

# 激活init
sess.run(init)

# 逐步训练201次
for step in range(201):
	sess.run(train)
	if step%20 == 0:
		print(step,sess.run(Weights),sess.run(biases))
		
```

这就是一个最简单的TensorFlow项目的模型,开始并不知道,这个数值的大小,通过不停的训练,优化减少误差,然后到最后学习到非常接近的程度

输出

```
2018-10-20 00:05:54.585046: I tensorflow/core/platform/cpu_feature_guard.cc:141] Your CPU supports instructions that this TensorFlow binary was not compiled to use: SSE4.1 SSE4.2 AVX AVX2 FMA
2018-10-20 00:05:54.587066: I tensorflow/core/common_runtime/process_util.cc:69] Creating new thread pool with default inter op setting: 2. Tune using inter_op_parallelism_threads for best performance.
0 [ 0.43479788] [ 0.16530335]
20 [ 0.20066421] [ 0.24722558]
40 [ 0.13186473] [ 0.28329453]
60 [ 0.1100866] [ 0.29471198]
80 [ 0.10319287] [ 0.2983261]
100 [ 0.1010107] [ 0.29947013]
120 [ 0.10031993] [ 0.29983228]
140 [ 0.10010127] [ 0.29994693]
160 [ 0.10003206] [ 0.2999832]
180 [ 0.10001015] [ 0.29999468]
200 [ 0.10000321] [ 0.29999834]
```

这个Session从未知的数值开始跑,一直跑到非常接近

> # 以上只是一个非常简单的案例,除此之外所有的数据可能会出现高维的情况

所以我们要通过学习这些优化的原理来,解决更加复杂的问题

- 1.Session的控制

>我们尝试创建两个数组来学习Session的思考模式,这种创建好业务,通过其他方法来执行

**刚开始我也觉得挺难受的,但是随后你就会发现这种业务是实现分离的方式非常,有意义吧**

```python

import tensorflow as tf

matrix1 = tf.constant([[3,3]])
matrix2 = tf.constant([[2],[2]])

product = tf. matmul(matrix1,matrix2)

# Session控制
sess = tf.Session()

result = sess.run(product)

print(result)

sess.close()

```

返回结果

```
2018-10-20 00:15:07.840507: I tensorflow/core/platform/cpu_feature_guard.cc:141] Your CPU supports instructions that this TensorFlow binary was not compiled to use: SSE4.1 SSE4.2 AVX AVX2 FMA
2018-10-20 00:15:07.842911: I tensorflow/core/common_runtime/process_util.cc:69] Creating new thread pool with default inter op setting: 2. Tune using inter_op_parallelism_threads for best performance.
[[12]]

```
