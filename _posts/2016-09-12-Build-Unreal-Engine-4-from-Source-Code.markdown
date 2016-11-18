---
layout:     post
title:      "Build Unreal Engine 4"
subtitle:   "Build UE4 from Source Code"
date:       2016-09-12 12:00:00
author:     "Caedmom"
header-img: "img/in-post/default-bg.jpg"
tags:
    - Unreal Engine 4
---


## 1. 打开EpicGames的github页面
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/20160912-compile-unreal-engine-4/0%20download-zip.jpg?raw=true)

基于OpenGL标准开发的应用程序运行时需有动态链接库OpenGL32.DLL、Glu32.DLL，这两个文件在
安装Windows NT时已自动装载到C：\WINDOWS\SYSTEM32目录下(这里假定用户将Windows NT安装
在C盘上)。OpenGL的图形库函数封装在动态链接库OpenGL32.DLL中，开发基于OpenGL的应用程序，
必须先了解OpenGL的库函数。OpenGL函数命令方式十分有规律，每个库函数均有前缀gl、glu、
aux，分别表示该函数属于OpenGL基本库、实用库或辅助库。Windows NT下的OpenGL包含了100多
个核心函数，均以gl作为前缀，同时还支持另外四类函数：
    OpenGL实用库函数：43个，以glu作为前缀；
    OpenGL辅助库函数：31个，以aux作为前缀；
    Windows专用库函数(WGL)：6个，以wgl作为前缀；
    Win32API函数(WGL)：5个，无前缀。

另外网友反馈：如果是用C#的话，用OpenTK比较好。而且glut都老的不像样了。应该用glew +
glfw。现在要用OpenGL4，才能发挥显卡的性能，效果。

## 安装GLUT工具包
GLUT不是OpenGL所必须的，但它会给我们的学习带来一定的方便，推荐安装。
Windows环境下的GLUT下载： glutdlls37beta.zip（附件暂未上传）

GLUT代表OpenGL应用工具包，英文全称为OpenGL Utility Toolkit，是一个和窗口系统无关的
软件包，它由Mark Kilgard在SGI时写的。作为AUX库的功能更强大的替代品，用于隐藏不同窗口
系统API的复杂性。是一个学习OpenGL编程的一个良好开端。

## VS环境配置
将下载的压缩解压，将得到5个文件（glut.dll, glut32.dll, glut.lib, glut32.lib,glut.h）
（1）把glut.h复制到x:\Program Files\Microsoft Visual Studio 10.0\VC\include\gl
文件夹中,如果没有gl这个文件夹则可以自己新建一个。（x是你安装VS的盘符号）
（2）把解压得到的glut.lib和glut32.lib放到静态函数库所在文件夹（即与include并排的lib
文件夹下）。
（3）把解压得到的glut.dll和glut32.dll放到操作系统目录下面的system32文件夹内。
（典型的位置为：C:\Windows\System32）,64位系统请将glut32.dll放到
C:\Windows\SysWOW64目录下。
（注：如在开发应用程序时用到OpenGL辅助库函数，则还需下载相应动态链接库，包含glaux.dll,
 glaux.lib, glaux.h，相应步骤同上）

## 第一个OpenGL程序
首先创建工程，其步骤如下：
（1）创建一个Win32 Console Application。
（2）链接OpenGL libraries。在Visual C++中先右击项目，选择属性，找到连接器标签，最后在
输入中的附加依赖库加上opengl32.lib glut32.lib glu32.lib.

![img](/img/in-post/20160622teapot/teapot-project-attributes.jpg)

添加依赖的链接库（英文分号隔开）

![img](/img/in-post/20160622teapot/input-add-libs.jpg)

现在你可以把下面的例子拷贝到工程中去，编译运行。你可以看到一个绿色的teapot。

![img](/img/in-post/20160622teapot/teapot.jpg)

<pre><code>
`[c++]
#include "stdafx.h"
#include<gl/glut.h>
void init(void)
{
	glEnable(GL_DEPTH_TEST);

	GLfloat position[] = { 1.0, 1.0, 1.0, 0.0 };
	glLightfv(GL_LIGHT0, GL_POSITION, position);
	glEnable(GL_LIGHTING);
	glEnable(GL_LIGHT0);

	GLfloat ambient[] = { 0.0, 0.0, 0.0, 1.0 };
	GLfloat diffuse[] = { 0.25, 0.95, 0.5, 1.0 };
	GLfloat specular[] = { 1.0, 1.0, 1.0, 1.0 };
	glMaterialfv(GL_FRONT, GL_AMBIENT, ambient);
	glMaterialfv(GL_FRONT, GL_DIFFUSE, diffuse);
	glMaterialfv(GL_FRONT, GL_SPECULAR, specular);
	glMaterialf(GL_FRONT, GL_SHININESS, 50.0);
}
void display(void)
{
	glClearColor(0.75f, 0.75f, 0.75f, 1.0f);
	glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);

	glNewList(1, GL_COMPILE);
	glutSolidTeapot(0.5);
	glEndList();
	glCallList(1);

	glFlush();
}
void reshape(GLsizei w, GLsizei h)
{
	glViewport(0, 0, w, h);
	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	glOrtho(-1.0, 1.0, -1.0, 1.0, -1.0, 1.0);
	glMatrixMode(GL_MODELVIEW);
}
int main(int argc, char** argv)
{
	glutInit(&argc, argv);
	glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB | GLUT_DEPTH);
	glutInitWindowPosition(0, 0);
	glutInitWindowSize(500, 500);
	glutCreateWindow(argv[0]);
	init();
	glutReshapeFunc(reshape);
	glutDisplayFunc(display);
	glutMainLoop();
	return 0;
}
`
</code></pre>

如果出现error LNK1123: 转换到 COFF 期间失败: 文件无效或损坏，将XX:\Program Files (x86)\Microsoft Visual Studio 10.0\VC\bin目录下的cvtres.exe删除
更新一下,cvtres.zip(附件暂未上传)
