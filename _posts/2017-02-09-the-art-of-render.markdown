---
layout:     post
title:      "[Translation]The Art of Render"
subtitle:   "Architecture Render"
date:       2017-02-09 12:00:00
author:     "Caedmom"
header-img: "img/in-post/default-bg.jpg"
tags:
    - Render
    - Translation
---


## 【译文】渲染艺术-7种常见的建筑效果图风格
---

* 在以前渲染的效果图中，会将建筑展示在饱和度不高的天空下[译注1]；在歌剧院举办的高级定制服装秀中，超模们面无表情高冷地走着猫步，增加了歌剧院空间的排他性。这些模式仍然被广泛使用，但从早期的建筑渲染对比来看已经取得了重大的技术进步，现在的渲染允许适当的使用电影中的技巧：利用颜色、照明、构图等来表达人们的情绪情感。

* 以下几张图片为大家展示天空饱和度对效果图的影响：

![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/20170209-the-art-of-render/1.png?raw=true)
* 读者注意力都转移到云层上去了，干扰了对建筑物的欣赏。
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/20170209-the-art-of-render/2.png?raw=true)
* 这张换了一个阴天多云的场景，云层中有蓝天的间隙，太阳光从左上角摄入画面，使得图片有一个从亮到暗的国度。 

* 在选择了合适的背景图后，我们需要对其饱和度进行调节，使其更能融入画面，更完善地表达情感。
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/20170209-the-art-of-render/3.png?raw=true)
* 这张饱和度过高，从视觉上压到了建筑和地面，使得整个图片的主次关系不平衡。
![img]https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/20170209-the-art-of-render/4.png?raw=true
* 现在的图能够引导观赏者的视线从左边过渡到右边，穿过天桥，越过火车，想象画面中的人们向桥廊的另一端走去。原本看起来静止的画面产生了流动性和故事感。并且天空的饱和度顺势降低，在视觉上与建筑物和地面相平衡。

* 电影和建筑都有一个内在的共同点：故事讲述，述说一段历史，说明背后的寓意。这个共同点是我们使用计算机软件建模然后渲染效果图的基础。在建筑效果图渲染中，如果它的效果不能达到预期，表现不出吸引力或说服力，那么还不如就使用简单的示意图来替代。

* 从目前纷繁庞杂的视觉内容来看，现在的建筑表现，特别是渲染技术或渲染手法几乎固定了。计算机生成的图像不再是想法与其实现之间的中介，它本身就是一个成品。多年来出现了不同的渲染类型，在方法和风格上类似于电影中直观的效果。
---
* **1.1.2** 第二种情况是在父类中并不知道具体要实例化哪一个具体的子类：假设我们在类A中要使用类B，B是一个抽象父类，在A中并不知道具体要实例化B的哪一个子类，但是类A的子类D中是可以知道的。在A中我们没有办法使用类似于“new xxx；”的语句，因为根本就不知道 xxx 是什么。以上问题引出了Factory模式的两个最重要的功能： 

（1）定义创建对象的接口，封装了对象的创建；  
（2）使得具体化类的工作延迟到了子类中。 
 
* Factory模式不单是**提供了创建对象的接口**，其中最重要的是**延迟了子类的实例化**（第二种情况），第二种情况Factory的结构示意图： 

![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2016-12-01-design-pattern-factory/Factory2.png?raw=true)

* 这种Factory模式不只是为了封装对象的创建，而是要把对象的创建放到子类中实现：Factory中只是提供了对象创建的接口，其实现将放在Factory的子类ConcreteFactory中进行。这是两种Factory模式的结构示意图的区别所在。

---

### 讨论 

* Factory模式在实际开发中应用非常广泛，面向对象的系统经常面临着对象创建问题：要创建的类实在是太多了。而Factory提供的**创建对象的接口封装**（第一个功能），以及它**将类的实例化推迟到子类**（第二个功能）都部分地解决了实际问题，采用Factory模式后系统可读性和维护都变得elegant许多。
* Factory也带来至少以下两个问题： 

（1）如果为每一个具体的ConcreteProduct类的实例化提供一个函数体，那么我们可能不得不在系统中添加了一个方法来处理这个新建的ConcreteProduct，这样Factory的接口永远不可能封闭（Close）。当然我们可以通过创建一个Factory的子类来通过多态来实现这一点，但这也是以新建一个类作为代价的。  

（2）在实现中我们可以通过参数化工厂方法，即给FactoryMethod()传递一个参数用以决定创建哪一个具体的Product。当然也可以通过模板化避免（1）中的子类创建子类，其方法就是将具体Product类作为模板参数，实现起来也很简单。 

* 可以看出，Factory模式对于对象的创建给予开发人员提供了很好的实现策略，但是Factory模式**仅仅局限于一类类**（就是说Product是一类，有一个共同的基类）。 

* **如果我们要为不同类的类提供一个创建对象的接口，那就要用AbstractFactory了。**
