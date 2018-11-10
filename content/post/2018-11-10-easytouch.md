---
title: 手游开发EasyTouch的使用
author: DashJay
date: '2018-11-10'
slug: easytouch
categories:
  - Unity
tags:
  - 游戏
lastmod: '2018-11-10T16:18:20+08:00'
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

## EasyTouch是用来开发手机端程序的

> ## EasyTouch四和五提供了两种不同的方式来监听手上的操作
- - - -

个人虽然认为四版本的效率会高一点,但是听老大说,都一样,都是同一种的东西的不同实现

先说一下四版本的用法

### 1.首先我们需要在场景中添加EasyTouch这个组件来保证4版本的运行成功
<center><img src="/post/2018-11-10-easytouch_files/屏幕快照 2018-11-10 20.15.40.png" alt="" width="49%"/></center>


### 2.然后我们在代码中必须在Onenable里添加监听或者说委托

```
private void OnEnable(){
  EasyTouch.On_SimpleTap += delegate{
    Debug.log("我就点了一下")
  }
}
```

我们这样操作是可以达成目标的,但是有时候光添加不管删除总是容易造成错乱,因此我们常常写一个外部方法,在需要的时候进行调用

```
    //开始初始化,添加监听
    private void OnEnable()
    {
        EasyTouch.On_SimpleTap += OneClick;
    }

    //结束时候关闭监听
    private void OnDestroy()
    {
        EasyTouch.On_SimpleTap -= OneClick;
    }

    static void OneClick(Gesture gesture)
    {
        Debug.Log("w偶就点了一下咋地");
    }
```

这是C#的一种特性,类似于委托,类似于Addlistener那一套都是一样的东西
- - - - 
我觉得上方的方法效率会高一些,但是实际开发中往往使用一下方法

### 3.Easytouch5代的新特性

五代的新特性中无需使用监听的方法了,他直接使用类似于inpiut的方法,效果非常好,开发省时省力

```
void Update()
    {
        Gesture CurrentGestrue = EasyTouch.current;

        if (EasyTouch.EvtType.On_SimpleTap == CurrentGestrue.type)
        {
            print("我也就点了一下啊")
        } 
    }
```
以上方法一样可以达到目的,但是我不知道为啥我就是感觉他比之前的方法慢了那么一点,因此我还是,为了偷懒,使用第二种五代方法吧

> # 真香

以上主要说的都是,其实对屏幕的操控,其他的按钮,或者其他的Stick类的东西都可以使用同样的方法,是不是超级牛逼

