---
layout:     post
title:      "Build Unreal Engine 4"
subtitle:   "Build Unreal Engine 4 from Source Code"
date:       2016-09-12 12:00:00
author:     "Caedmom"
header-img: "img/in-post/default-bg.jpg"
tags:
    - Unreal Engine 4
---

## 1. 资源下载与操作

---

* 1.1. 打开EpicGames的github页面，下载zip文件（大约184MB）
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/20160912-compile-unreal-engine-4/0%20download-zip.jpg?raw=true)

* 1.2. 解压zip文件，点击运行`Setup.bat`
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/20160912-compile-unreal-engine-4/1%20click-setup.bat.gif?raw=true)

* 1.3. 检测和更新依赖项（大约1-2小时）
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/20160912-compile-unreal-engine-4/2%20update-dependencies.gif?raw=true)

* 1.4. 生成解决方案
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/20160912-compile-unreal-engine-4/3%20click-generate-project-files.bat.gif?raw=true)

---

## 2. 编译引擎

---

* 2.1 双击 UE4.sln 文件，在 Visual Studio 中加载所有项目。
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/20160912-compile-unreal-engine-4/3%20click-generate-project-files.bat.gif?raw=true)

* 2.2 将方案的配置选为 Development Editor，将方案的平台选为 Win64.
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/20160912-compile-unreal-engine-4/5%20set-dev-editor-and-win64.png?raw=true)

* 2.3 右键点击 UE4 并选择 Build（根据配置不同，耗时约20分钟-2小时），引擎编译完成后，将默认启动项目设置为 UE4。
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/20160912-compile-unreal-engine-4/6%20build-and-set-start-project.png?raw=true)

* 2.4 调试项目
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/20160912-compile-unreal-engine-4/7%20debug-start-new-instance.png?raw=true)
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/20160912-compile-unreal-engine-4/7%202-debug.png?raw=true)

* 在调试完成后自动启动编辑器