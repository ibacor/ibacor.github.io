---
layout: post
title: "组合模式"
date: 2019-12-21
description: "组合模式"
tag: 设计模式
---  

适配器模式是很常用的设计模式，解决不同系统、层次对接时经常会用到它。
#### 定义
> 将对象组合成树形结构以表示“部分-整体”的层次结构，使得用户对单个对象和组合对象的使用具有一致性。

通用类图如下：  
![](/images/posts/designpattern/composite1.png)  
类图中包含2个角色：  
Component抽象构件定义组合对象共有的方法和属性，它是组合模式的精髓；  
Composite树枝对象是组合模式的重点，它的作用是组合树枝节点和叶子结点形成一个树形结构；  
Leaf叶子对象是遍历的最小单位，定义参加组合的原始对象行为

#### 优点
1. 高层模块调用简单
2. 叶子模块可以自由增加

#### 缺点
- 直接使用实现类，破坏依赖倒置原则

#### 使用场景
- 当出现树形结构时

#### 拓展
透明的组合模式——组合模式的另一种实现。通用类图如下：  
![](/images/posts/designpattern/composite2.png)  

参考：
> 设计模式之禅