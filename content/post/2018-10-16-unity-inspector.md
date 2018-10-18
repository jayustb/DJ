---
title: 尝试对Unity中的Inspector面板进行修改
author: ''
date: '2018-10-16'
slug: unity-inspector
categories:
  - Untiy
  - Editor
tags:
  - Editor
lastmod: '2018-10-16T17:55:34+08:00'
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

- - - -
我们在有些时候需要对Inspector面板中某些功能进行修改比如添加一些下拉菜单之类的,然后我们针对Map这个脚本,在Editor中创建了一个脚本
起了个名字叫做`MapEdit.cs`,必须引入一下头文件

```C#
using UnityEditor;
using UnityEngine;
```

在该类之前一定要使用`[CustomEditor(typeof(Map))]`字段,来重写对他的面板的实现

那么该MapEdit类必须继承Editor并且不继承Monobehavior

```
public class MapEditor : Editor
```

# 我重新说一下以上我们做的事和以下做的

### 1.创建一个类继承于Editor

### 2.在该类上方声明`[CustomEditor(typeof(Map))]`

讲了半天就讲了这么一点
- - - -
### 3.以下我们首先对原本Inspector的实现

```
base.OnInspectorGUI();
```
这样原来的选项都还在
<img src="/post/2018-10-16-unity-inspector_files/屏幕快照 2018-10-17 00.07.20.png" alt="" width="99%"/>

原来该是啥样还是啥样

### 4.接下来我添加一段演示代码

```Csharp

[CustomEditor(typeof(Map))]
public class MapEditor : Editor
{
    public override void OnInspectorGUI()
    {
        base.OnInspectorGUI();

        //绘制一个水平区域
        EditorGUILayout.BeginHorizontal();

        var currentIndex = EditorGUILayout.Popup(0, new string[] {"a", "b"});

        if (GUILayout.Button("读取列表"))
        {
        }

        EditorGUILayout.EndHorizontal();
    }
}

```

该类整体如上所示

<img src="/post/2018-10-16-unity-inspector_files/屏幕快照 2018-10-17 00.09.23.png" alt="" width="99%"/>

<img src="/post/2018-10-16-unity-inspector_files/屏幕快照 2018-10-17 00.09.28.png" alt="" width="99%"/>



