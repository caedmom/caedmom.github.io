---
layout:     post
title:      "Design Pattern - Factory"
subtitle:   "Creational Pattern"
date:       2016-11-30 12:00:00
author:     "Caedmom"
header-img: "img/in-post/default-bg.jpg"
tags:
    - Design Pattern
    - C++
---


## 1. 创建型模式
---

### 1.1. 工厂（Factory）模式

---
* **1.1.1.** 为了提高**内聚（Cohesion）**和松**耦合（Coupling）**，我们经常会**抽象出一些类的公共接口以形成抽象基类或者接口**。这样我们**可以通过声明一个指向基类的指针来指向实际的子类实现，达到了多态的目的。
* n多个子类继承自抽象基类，我们不得不在每次用到子类的地方就编写诸如“ new xxx ；”的代码，引入两个问题： 

（1）客户端程序员必须知道实际子类的名称（当系统复杂后，命名将是一个很不好处理的问题）；
（2）程序的扩展性和维护变得越来越困难。 

对于 1.1.1 这种情况，我们经常就是**声明一个创建对象的接口，并封装了对象的创建的过程**。Factory这里类似于一个真正意义上的工厂（生产对象）。第一种情况Factory的结构示意图： 
![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2016-12-01-design-pattern-factory/Factory1.png?raw=true)
* **这种Factory模式经常在系统开发中用到**，但这并不是Factory模式的最大威力所在（因为可以通过其他方式解决这个问题）。

---
* **1.1.2** 第二种情况是在父类中并不知道具体要实例化哪一个具体的子类：假设我们在类A中要使用类B，B是一个抽象父类，在A中并不知道具体要实例化B的哪一个子类，但是类A的子类D中是可以知道的。在A中我们没有办法使用类似于“new xxx；”的语句，因为根本就不知道 xxx 是什么。以上问题引出了Factory模式的两个最重要的功能： 

（1）定义创建对象的接口，封装了对象的创建；  
（2）使得具体化类的工作延迟到了子类中。 
 
* Factory模式不单是**提供了创建对象的接口**，其中最重要的是**延迟了子类的实例化**（第二种情况），第二种情况Factory的结构示意图： 

![img](https://github.com/caedmom/caedmom.github.io/blob/master/img/in-post/2016-12-01-design-pattern-factory/Factory2.png?raw=true)

* 这种Factory模式不只是为了封装对象的创建，而是要把对象的创建放到子类中实现：Factory中只是提供了对象创建的接口，其实现将放在Factory的子类ConcreteFactory中进行。这是两种Factory模式的结构示意图的区别所在。

---
### 讨论：
* Factory模式在实际开发中应用非常广泛，面向对象的系统经常面临着对象创建问题：要创建的类实在是太多了。而Factory提供的**创建对象的接口封装**（第一个功能），以及它**将类的实例化推迟到子类**（第二个功能）都部分地解决了实际问题，采用Factory模式后系统可读性和维护都变得elegant许多。
* Factory也带来至少以下两个问题： 

（1）如果为每一个具体的ConcreteProduct类的实例化提供一个函数体，那么我们可能不得不在系统中添加了一个方法来处理这个新建的ConcreteProduct，这样Factory的接口永远不可能封闭（Close）。当然我们可以通过创建一个Factory的子类来通过多态来实现这一点，但这也是以新建一个类作为代价的。 
（2）在实现中我们可以通过参数化工厂方法，寄给FactoryMethod（）传递一个参数用以决定创建哪一个具体的Product。当然也可以通过模板化避免（1）中的子类创建子类，其方法就是将具体Product类作为模板参数，实现起来也很简单。
* 可以看出，Factory模式对于对象的创建给予开发人员提供了很好的实现策略，但是Factory模式**仅仅局限于一类类**（就是说Product是一类，有一个共同的基类）。
* **如果我们要为不同类的类提供一个创建对象的接口，那就要用AbstractFactory了。**

---
`C++`
* 代码片断 1： `Product.h`
<pre><code>//Product.h
#ifndef _PRODUCT_H_
#define _PRODUCT_H_
class Product
{
public:
virtual ~Product() =0;
protected:
Product();
private:
};
class ConcreteProduct:publicProduct
{
public:
~ConcreteProduct();
ConcreteProduct();
protected:
private:
};
#endif //~_PRODUCT_H_
</code></pre>

* 代码片断 2： `Product.cpp`
<pre><code>//Product.cpp
#include "Product.h"
#include<iostream>
using namespace std;
Product::Product()
{
}
Product::~Product()
{
}
ConcreteProduct::ConcreteProduct()
{
cout<<"ConcreteProduct...."<<endl;
}
ConcreteProduct::~ConcreteProduct()
{
}
</code></pre> 


* 代码片断 3： `Factory.h`
<pre><code>//Factory.h
#ifndef _FACTORY_H_
#define _FACTORY_H_
class Product;
class Factory
{
public:
virtual ~Factory() = 0;
virtual Product* CreateProduct() = 0;
protected:
Factory();
private:
};
class ConcreteFactory:public Factory
{
public:
~ConcreteFactory();
ConcreteFactory();
Product* CreateProduct();
protected:
private:
};
#endif //~_FACTORY_H_
</code></pre> 


* 代码片断 4： `Factory.cpp`
<pre><code>//Factory.cpp
#include "Factory.h"
#include "Product.h"
#include <iostream>
using namespace std;
Factory::Factory()
{
}
Factory::~Factory()
{
}
ConcreteFactory::ConcreteFactory()
{
cout<<"ConcreteFactory....."<<endl;
}
ConcreteFactory::~ConcreteFactory()
{
}
Product* ConcreteFactory::CreateProduct()
{
return new ConcreteProduct();
}
</code></pre> 


* 代码片断 5： `main.cpp`
<pre><code>//main.cpp
#include "Factory.h"
#include "Product.h"
#include <iostream>
using namespace std;
int main(int argc,char* argv[])
{
Factory* fac = new ConcreteFactory();
Product* p = fac->CreateProduct();
return 0;
}
</code></pre>