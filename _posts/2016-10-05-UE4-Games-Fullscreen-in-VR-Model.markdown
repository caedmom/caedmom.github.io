---
layout:     post
title:      "UE4-Games Fullscreen in VR Model"
subtitle:   "How to Set UE4-Games Fullscreen in VR Model"
date:       2016-10-05 12:00:00
author:     "Caedmom"
header-img: "img/in-post/default-bg.jpg"
tags:
    - Unreal Engine 4
    - VR
---


## 1. 重新编译引擎
---

* 编译和非编译的最大区别在于，你可以对UE4的底层源码进行修改，添加你自己的设置，如果这样不明白的话，举个例子。就是UE4 VR预览模式一直以来都是两边是黑色的，我们无法去改动，这是官方下载的非编译版的问题。因为它不能修改源码，所以就算你知道哪里有问题，也不能改动。

* 而编译版呢，区别在于，我知道哪里出问题了，我就可以在那里进行改动，就说回这个VR模式，黑边的问题，编译后的文件夹中，找到UE4.slh，打开，我们搜索  SteamVRRender.Cpp，找到SteamVRRender.cpp文件。
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2016-10-05-UE4-games-fullscreen-in-VR-model/0%20find-cpp-file.png?raw=true)

* 找到要修改的代码段
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2016-10-05-UE4-games-fullscreen-in-VR-model/1%20source-code.png?raw=true)

* 修改代码
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2016-10-05-UE4-games-fullscreen-in-VR-model/2%20modify-source-code.png?raw=true)

* 然后在第一张图的列表中找到UE4，右键出现菜单后，选择“生成”，再然后点击“本地Windows调试器”，此过程结束后将自动打开编译好的UE4editor。（可参考上一篇“Build Unreal Engine 4”）

* 未编译版本效果图
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2016-10-05-UE4-games-fullscreen-in-VR-model/3%20VR-model-view-with-black-.png?raw=true)

* 编译版本效果图，现在在虚拟现实模式下预览就可以全屏了。
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2016-10-05-UE4-games-fullscreen-in-VR-model/4%20fullscreen.png?raw=true)

* 注：如果只是修改坐标（0.0f,0.3f,0.4f,0.4f）,ViewportWidth和ViewHeight不变，则只能将视野加宽，无法去掉黑边。
---

## 2. 其它

---

* 如果还未全屏，可能还需要在UE4编辑器中进行设置。

* 打开关卡蓝图
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2016-10-05-UE4-games-fullscreen-in-VR-model/5%20level-blueprint.png?raw=true)

* 配置工程目录
设置配置文件在工程目录里面找到 Config 文件夹在里面添加一个配置文件并命名为 DefaultGameUserSettings.ini

* 把如下内容贴到刚刚创建的配置文件里面：
`ini`
<pre><code>
[/Script/Engine.GameUserSettings]
bUseVSync=False
//ResolutionSizeX=1920
//ResolutionSizeY=1080
//LastUserConfirmedResolutionSizeX=1920
//LastUserConfirmedResolutionSizeY=1080
WindowPosX=-1
WindowPosY=-1
bUseDesktopResolutionForFullscreen=True
FullscreenMode=0
LastConfirmedFullscreenMode=0
Version=5
</code></pre>

---