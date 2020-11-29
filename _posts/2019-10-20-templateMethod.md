---
layout: post
title: "模板模式"
date: 2018-10-20
description: "模板模式"
tag: 设计模式
---  

模板模式是一个相当简单的设计模式，很多使用java的人已经不自觉的用过了，因为它就是这个情景：在抽象类中定义和使用抽象方法，抽象方法在子类中具体实现，这种结构固定实现方法在子类中完成的方法就叫模板模式。
#### 定义
定义一个操作中的算法的框架，而将一些步骤延迟到子类中，使得子类可以不改变一个算法的结构即可重定义某些特定步骤。通用类图如下：  
![](/images/posts/designpattern/templateMethod.png)  
AbstractClass叫模板抽象类，里面的方法分为两种：*基本方法*和*模板方法*，其中基本方法由子类负责实现，模板方法完成对基本方法对调度，为了安全，**一般会用final修饰防止篡改**。
#### 优点
模板方法将可变部分通过继承机制由子类实现，提取出公共部分代码，便于维护；并且行为是由父类控制，有利于统一。
#### 缺点
每一个不同的实现都要由子类继承来实现，最终可能导致系统更加庞大。
#### 其他
模板模式让人想起来父类调用子类的方法。Java中另外的调用子类的方法有：

1. 把子类传经父类的有参构造方法  
2. 通过反射
3. 调用子类的静态方法

参考
> 设计模式之禅