---
layout:     post
title:      "Unity NGUI Slide"
subtitle:   "Make Slide by Change Materials"
date:       2014-12-23 12:00:00
author:     "Caedmom"
header-img: "img/in-post/unity-bg.jpg"
tags:
    - Unity
    - NGUI
---


## 效果图 

---
* 本文使用NGUI制作按钮，通过点击按钮，改变Cube(或其他带有MeshRenderer组件的对象)的材质来达到切换图片的效果。 
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/0%20SlidePictures.gif?raw=true) 

---

## 操作步骤 

---

* 1.新建工程，导入NGUI插件。 

* 2.随意创建一个对象（如sprite），以创建UI Root,NGUI>>Create>>Sprite,删除Main Camera。
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/1%20UI-Root.png?raw=true) 

* 3.为了方便编辑，取消勾选Camera，让它暂时处于未激活状态 
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/2%20UI-shelter-from-camera.png?raw=true) 

![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/3%20set-active-false.png?raw=true) 

![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/4%20camera-has-set-active-false.png?raw=true) 

* 4.删除之前创建的sprite，在UI Root中创建一个Panel(用它来当容器，装之后创建的子对象)，选中UI Root>>NGUI>>Create>>Panel
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/5%20create-panel.png?raw=true) 

* 5.选中Panel，创建Sprite(在场景中右键快捷创建或者NGUI>>Create>>Sprite创建)，命名为Button-Next,将它拖放到合适位置。
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/6%20create-sprite.png?raw=true) 

* 6.选中Sprite,设置Atlas>>设置Sprite>>设置Sprite Type为Sliced(如果不做这个设置，后续添加碰撞器时将报错)
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/7%20set-sprite.png?raw=true) 

* 7.添加一个碰撞器，然后再添加Button脚本
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/8%20attach-collider.png?raw=true) 

![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/9%20attach-button-script.png?raw=true) 

* 8.创建一个lable用于显示按钮名称
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/10%20create-child-label.png?raw=true) 

* 9.导入图片制作材质
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/11%20import-textures-and-make-materials.png?raw=true) 

* 10.添加一个Cube(其它有Mesh Renderer的对象也行)，设置大小和旋转，使得播放时能够看到图片，这里要注意的是，需要在3D模式下将Cube往UI层靠后拖动，以免挡住按钮UI,相机的CullingMask选择Everything
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/12%20set-cube-transform.png?raw=true) 

![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/10-2%20depth.png?raw=true) 

![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/13%20set-camera-culling-mask.png?raw=true) 

* 11.为Cube添加脚本SlideCube.cs（代码附于博文最后）

* 12.添加完成后为数组Mats手动附上材质
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/14%20give-mateials-to-cube.png?raw=true) 

* 13.运行发现图片有些黑，为场景添加平行光即可
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/15%20add-directional-light.png?raw=true) 

---

## 优化

---

* 14.你肯定会发现使用GetComponentsInChildren<UIButton>()获取到的button的顺序是按照添加顺序来定的，这样太不稳定了，而且将button（UI）作为cube(gameobject)的子物体后，调整起来很不方便，改进代码附于博文最后。 

* 15.将Cube拖拽到UI Button上，选择函数。
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/16%20drag-cube-to-UIButton.png?raw=true) 

* 16.选择函数前后对比：
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/17%20select-function-before.png?raw=true) 

![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/18%20select-function-after.png?raw=true) 

* 17.项目视图
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/19%20final-project.png?raw=true) 

---

## 拓展
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2014-12-03-unity-ngui-slide/NGUI-example.gif?raw=true) 

---

## 代码

---
`C#` 

---
<pre><code>//* 代码片断 1：初始代码
using UnityEngine;
using System.Collections;

public class SlideCube : MonoBehaviour {
	
	public Material[] mats;
	
	private UIButton[] btns;
	//private UIButton btn_back;
	private int index = 0;
	private Renderer render;
	

	// Use this for initialization
	void Start () {

		btns = this.GetComponentsInChildren<UIButton>();
		//btn_back = this.GetComponentInChildren<UIButton>();
		render=this.GetComponent<MeshRenderer>();
				
	}
	
	// Update is called once per frame
	void Update () {
		
		EventDelegate.Add (btns[0].onClick,delegate() {
			Debug.Log("click");
			index=index==mats.Length-1?0:index+1;
			Render();
		});


		EventDelegate.Add (btns[1].onClick,delegate() {
			Debug.Log("click");
			index=index==0?mats.Length-1:index-1;
			Render();
		});

		
	}
	
	void Render(){
		
		render.material = mats[index];
	}
}


//* 代码片断 2：改进代码
using UnityEngine;
using System.Collections;

public class SlideCube : MonoBehaviour {
	
	public Material[] mats;
	
	//private UIButton[] btns;
	//private UIButton btn_back;
	private int index = 0;
	private Renderer render;
	

	// Use this for initialization
	void Start () {

		//btns = this.GetComponentsInChildren<UIButton>();
		//btn_back = this.GetComponentInChildren<UIButton>();
		render=this.GetComponent<MeshRenderer>();
		
		
		
	}
	
	// Update is called once per frame
	void Update () {
		
		Next ();
		Back ();
		Render();

		
	}

	public void Next(){
		/*
		EventDelegate.Add (btns[0].onClick,delegate() {
			Debug.Log("click");
		index=index==mats.Length-1?0:index+1;
			Render();
		});
		*/
		index=index==mats.Length-1?0:index+1;
	
	}

	public void Back(){
		/*
		EventDelegate.Add (btns[1].onClick,delegate() {
			Debug.Log("click");
		index=index==0?mats.Length-1:index-1;
			Render();
		});
		*/
		index=index==0?mats.Length-1:index-1;
		
	}
	
	void Render(){
		
		render.material = mats[index];
	}
}


</code></pre> 