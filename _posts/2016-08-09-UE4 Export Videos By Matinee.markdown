---
layout:     post
title:      "UE4 Export Videos By Matinee"
subtitle:   "Export Videos From Unreal Engine 4 By Matinee"
date:       2016-08-09 12:00:00
author:     "Caedmom"
header-img: "img/in-post/default-bg.jpg"
tags:
    - UE4
    - Matinee
---


## 如何输出的视频？ 音乐是用什么软件配上去的呢？
* matinee做摄像机动画并导出序列，音乐以及序列合成视频是用AffterEffects做的。
 
## 导出序列和导出视频有什么区别？
* 导出视频就相当于在录屏，最终输出的是视频，那么你录制运行时如果卡顿的话，都会被录制下来，而导出序列最终输出的是图片序列，录制运行时候就算卡顿不是很流畅，但是序列是严格按照摄像机动画设定的秒数去记录每一帧的，所以导入到后期软件做合成的时候，动画播放时流畅的。
 
## 下面开始讲解UE4 Matinee录制视频

### Matinee相机设置
 
1.1. 过场动画>>添加Matinee
![img](/img/in-post/UE4-Export-Videos-By-Matinee/1 add-atinee.png)
1.2. 进入MatineeActor界面，点击Curves，将最大化轨迹（Tracks）界面
![img](/img/in-post/UE4-Export-Videos-By-Matinee/2 adjust-workspace.png)
1.3. 最大化轨迹标签效果如下图；时间轴可以调整，点击snap可以对齐，对齐设置中可以预设每次调整时间轴时的步长。
![img](/img/in-post/UE4-Export-Videos-By-Matinee/3 adjust-timeline-step.png)
1.4. 在关卡中将相机调整到合适位置和角度（这一步很重要，将决定录制的视频的起始画面），回到MatineeActor添加摄像机组。
 ![img](/img/in-post/UE4-Export-Videos-By-Matinee/4 add-camera-group.png)
 
1.5. 重命名摄像机组
![img](/img/in-post/UE4-Export-Videos-By-Matinee/5 rename-camera-group.png)
![img](/img/in-post/UE4-Export-Videos-By-Matinee/5 rename-camera-group2.png) 

 
1.6. 现在可以看到添加的摄像机和预览视角
![img](/img/in-post/UE4-Export-Videos-By-Matinee/6 preview.png)
 
1.7. 选中关键帧
![img](/img/in-post/UE4-Export-Videos-By-Matinee/7 add-key-frame.png)

1.8. 将时间标尺移到5秒处（移动时间轴、控制此段动画时长为5秒）
![img](/img/in-post/UE4-Export-Videos-By-Matinee/8 moving-timeline-keep-5-seconds.png)

1.9. 在关卡中移动相机，添加关键帧
![img](/img/in-post/UE4-Export-Videos-By-Matinee/10 add-key-frame.png)
* 可以点击预览效果。（相机的视野也可以修改）

1.11 添加DirGroup和关键帧，切换相机1和2.
![img](/img/in-post/UE4-Export-Videos-By-Matinee/11 add-dirgroup-and-key-frame.png)
 
参考资料：
https://www.youtube.com/watch?v=r9Rz_-Q5ZyY&index=26&list=PLshGCQ6KS0hF3PxMGzWiJ5ZaPxwKrOm5I
 
 
 
### 2.输出视频蓝图
2.1 选中刚才编辑的MatineeActor,在细节面板中勾选Play on Level Load,在运行程序时，首先会运行这段动画。
![img](/img/in-post/UE4-Export-Videos-By-Matinee/13 output-settings.png)
 
2.2 设置玩家默认起点
![img](/img/in-post/UE4-Export-Videos-By-Matinee/14 setting-player-start.png)
 
2.3 在动画结束后，可以到一个比较好的位置重新开始。玩家起始效果图：
![img](/img/in-post/UE4-Export-Videos-By-Matinee/15 player-start-view.png)
 
2.4 如果我们仅仅是为了录制视频，那么就需要在动画结束后停止而不进入程序。下面在蓝图中设置以便退出游戏。跳出录制蓝图：
![img](/img/in-post/UE4-Export-Videos-By-Matinee/15 jump-out-record.png)
* 进阶蓝图 
![img](/img/in-post/UE4-Export-Videos-By-Matinee/16 advanced-blueprint.jpg)
 
参考资料：
https://www.youtube.com/watch?v=wgk9hUtC-ig&list=PLshGCQ6KS0hF3PxMGzWiJ5ZaPxwKrOm5I&index=27
 
### 3.导出视频
* 渲染视频设置>>捕获视频

![img](/img/in-post/UE4-Export-Videos-By-Matinee/17 capture-video-and-output.png)

<iframe frameborder="0" width="100%" height="498" src="https://v.qq.com/iframe/player.html?vid=m034717et3g&tiny=0&auto=0" allowfullscreen></iframe>

注：保存的动画不带音效，需后期进行添加。
