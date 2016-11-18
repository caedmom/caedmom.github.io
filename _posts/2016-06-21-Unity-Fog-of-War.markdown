---
layout:     post
title:      "Unity Fog of War"
subtitle:   "unity plug-in"
date:       2016-06-21 12:00:00
author:     "Caedmom"
header-img: "img/in-post/unity-bg.jpg"
tags:
    - Unity
    
---


## 使用Tasharen Fog of War插件实现战争迷雾

先上效果图：

![img](/img/in-post/20160622fog-of-war/fog-of-war-advanced.gif)

接下来下载使用Tasharen Fog of War1.0插件，做了个小demo，写帖子时参考了这篇文档，感谢！

## 1.导入插件
![img](/img/in-post/20160622fog-of-war/1inport-plug-in.png)


## 2.将插件自带的Fog of War预设拖入场景
接着创建一个地形,和两个Cube，一个是CubeRedEnemy（以下简称Enemy）为红色，一个是CubeGreenHero（以下简称Hero）为绿色（颜色不重要），我们Hero移动来观Enemy的显现，接着让MainCamera俯Hero。

![img](/img/in-post/20160622fog-of-war/2drag-fog-of-war.png)

关于移动脚本大家可以自己编写简单的，也可以参考下我这个比较繁琐的脚本，大家使用时一定要记得给地形Terrain、CubeGreenHero、CubeRedEnemy分别打标签为Ground、Player、Enemy，否则你点不动哦~

## 3.添加插件中的脚本：
MainCamera：添加 FowEffect.cs – 使得摄像机得到渲染
Hero:添加 FOWRevealer.cs –控制主角可见范围
Enemy:添加 FOW Renderers.cs –控制阴影中是否可见
然后，将Hero下挂在的FOWRevealer脚本属性中Line Of Sight Check改为Every Update()

![img](/img/in-post/20160622fog-of-war/3setting-function.png)

## 4.运行
在demo中移动方块，你会发现已经有战争迷雾效果了，并且靠近Enemy时,Enemy会显现，远离时Enemy会消失在迷雾中 .（unity5.0中有Bug，可以尝试在Edit的Project Setting的player中把DX11取消勾选）

![img](/img/in-post/20160622fog-of-war/fog-of-war-demo.gif)

---

最后附上插件下载地址：链接：http://pan.baidu.com/s/1c4uwX4 密码：yaew，感谢支持！
