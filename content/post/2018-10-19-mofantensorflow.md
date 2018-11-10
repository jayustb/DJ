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

- - - -
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

>我可以使用另一种运行方法,来自动关闭Session

```python

with tf.Session() as sess:
	result2 = sess.run(product)
	print(result2)
	
```

这样也可以得到结果,[[12]]

- - - -
- 2.Variable控制使用

```python
import tensorflow as tf

# 创建了一个名字叫做Counter的变量0
state = tf.Variable(0,name='counter')

# one这个常量就是1
one = tf.constant(1)

# 新的数值是等于前一个数值加一的
new_value = tf.add(state,one)

#然后给新变量赋值
update = tf.assign(state,new_value)

#初始化所有数据
init = tf.global_variables_initializer()

# 开始Session
with tf.Session() as sess:
    # 数据初始化
    sess.run(init)
    #循环三次
    for _ in range(3):
        sess.run(update)
        print(sess.run(state))
```
Variable还真的就是Variable,不能用普通的常数代替

- - - -
- 3.PlaceHolder的用途

我们可以在写代码的时候不考虑输入的情况,然后在最后运算的时候输入说需要的数据

```python

import tensorflow as tf

# 首先给定类型，大部分情况都只处理float32
input1 = tf.placeholder(tf.float32)
input2 = tf.placeholder(tf.float32)

output = tf.multiply(input1, input2)

with tf.Session() as sess:
    print(sess.run(output, feed_dict={input1: [7], input2: [2]}))

```

>注意几点:都是以字典的形式输入的

- 4.激励函数

什么是激励函数的:不能使用线性解决的问题就可以用

>例子:女生非常漂亮都是时候,更多男生会喜欢这个女生这句话,但是假设当阿女生接近无限漂亮的时候,是不可能出现无数个男生喜欢这个女生的,因为男生的数量也有限,

以上就是我们生活中一个常见的非线性案例

<img src="/post/2018-10-19-mofantensorflow_files/屏幕快照 2018-10-20 01.32.46.png" alt="" width="50%"/>


在卷积中推荐:relu

循环神经网络中推荐relu和tanh

到时什么是激励函数呢?

你可以选择让一部分神经元激励,一部分不激励,来满足需求

<center><img src="/post/2018-10-19-mofantensorflow_files/屏幕快照 2018-10-20 01.37.14.png" alt="" width="40%"/></center>

除了线性的激励函数之外还有很多激励函数的›

<img src="/post/2018-10-19-mofantensorflow_files/屏幕快照 2018-10-20 01.38.40.png" alt="" width="80%"/>

<img src="/post/2018-10-19-mofantensorflow_files/屏幕快照 2018-10-20 01.39.20.png" alt="" width="80%"/>