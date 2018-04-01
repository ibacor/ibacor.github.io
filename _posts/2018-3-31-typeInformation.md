---
layout: post
title: "类型信息"
date: 2018-3-31
description: "类型信息"
tag: think in java 读书笔记 
---  

在运行时我们如何识别类和对象的信息呢？一般有两种方式：
+ “传统”RTTI，假定编译时已经知道所有类型信息
+ “反射”机制，运行运行时发现使用类的信息

### Class对象
可通过```forName()```创建Class引用
类字面常量——另一种生成对class对象的引用：```Name.class```

### 类型转换前的检查
instanceof：返回对象是否是某个特定类型的实例

### 反射：运行时的类信息
与RTTI的区别：RTTI在编译时打开和检查.class文件，反射是在运行时检查