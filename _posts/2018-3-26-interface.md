---
layout: post
title: "接口"
date: 2018-3-26
description: "接口"
tag: think in java 读书笔记 
---  
    接口和内部类为我们提供了一种将接口与实现分离的更加结构化的方法。
### 抽象类和抽象方法
形如```abstract void f();```的方法称为抽象方法。抽象方法是不完整的，只有声明没有方法体（注意不是空函数的意思）。而含有抽象方法的类就叫**抽象类**。如果一个类想从抽象类中继承，就必须为所有抽象方法提供定义。

### 接口
接口在抽象的概念上走得更远。抽象类允许有非抽象方法，而接口里面所有方法都只声明而没有方法体。接口的访问权限有两种：public和包访问权限。如果接口里面含有数据域，则这些域是隐式地是static和final的。接口里面的方法都是public的。

### 多重继承
java无法继承多个类，但可以使用接口来实现这个功能。通过实现（implements），能够向上转型为多个基类型。

### 通过继承扩展接口
接口可以使用继承，用法同样通过extends关键字。有这样一个例子：
```
interface Monster{
    void menace();
}

interface Lethal{
    void kill();
}

interface DangerousMonster extends Monster,Lethal{
    void destroy();
}
```
这里extends后面有个逗号，但是这样的情况也只适用于接口。

### 接口和工厂
利用接口的向上转型以及面向对象的多态特性，可以使用*工厂方法*返回合适的对象。
另外，接口里面也可以包含接口，也即接口是多层嵌套的。