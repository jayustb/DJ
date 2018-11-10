---
title: delegate委托,事件EventHandler使用
author: DashJay
date: '2018-10-24'
slug: delegate-eventhandler
categories:
  - Unity
tags:
  - 游戏
lastmod: '2018-10-24T00:49:42+08:00'
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

> # 为了实现鼠标的点击事件,和处理逻辑分离,我们通常这样做

创建一个类,继承与`EventArgs`,

```
//鼠标点击参数类
public class TileClickEventArgs : EventArgs
{
    //0左键,1右键
    private int MouseButton;

    //地图块
    private Tile Tile;

    public TileClickEventArgs(int mouseButton, Tile tile)
    {
        MouseButton = mouseButton;
        Tile = tile;
    }
}
```

我们先把他实例化出来

```
//系统啊自带的委托,使用泛型来创建,事件是委托的实例
public event EventHandler<TileClickEventArgs> OnTileClick;

```

在UPdate中实时监测

```
    private void Update()
    {
        //检测鼠标左键
        if (Input.GetMouseButtonDown(0))
        {
            //TODO:把鼠标的点击事件,和相关的处理逻辑分离
            //获取鼠标下方的地图
            var t = GetTileUnderMouse();
            if (t != null)
            {
                //创建新的点击事件
                var e = new TileClickEventArgs(0, t);

                // 如果点到了地图
                if (OnTileClick != null)
                {
                    //
                    OnTileClick(this, e);
                }
            }
        }
    }
```

其实以上就是一个C#,的事件的标准样式

从定义,到触发,到处理,分层解决

逻辑和实现分离

```
//Map监听鼠标地事件
        OnTileClick += Map_OnTileClick;
```

```
    private void Map_OnTileClick(object sender, TileClickEventArgs e)
    {
        throw new NotImplementedException();
    }
```

这里已经多多少少设计C#的语法了,我也不是很明白,但是先这样理解是一件好事,因为,他就是这样处理一件事的MVC也就是这样处理的