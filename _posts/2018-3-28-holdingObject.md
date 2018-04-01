---
layout: post
title: "持有对象"
date: 2018-3-28
description: "容器的简单介绍"
tag: think in java 读书笔记 
---  

“如果一个程序只包含固定数量的且其生命周期都是已知的对象，那么这是一个简单的程序”。为了方便存放数量，java提供了一些“集合类”（也叫“容器类”）。

### 泛型和泛型安全的容器
容器顾名思义是容纳对象的，但是对象有很多种，如何保证存放的类型相同，或者更重要的取出来是哪个类型，就需要用到泛型。具体用法是使用```ArrayList<>```指定具体类型。

### 基本概念
总的来说，List、Set和Queue实现Collection接口，Map是单独一个
![](/images/posts/think_in_java/collection.png)

### 添加一组元素
可以把数组变为List，使用```Arrays.asList()```，如果要确定类型需要```List<Snow> snow4 = Arrays.<Snow>asList();```。
当需要添加一批元素时，可使用```addAll()```方法这是Collection接口的方法，实现了该接口的集合类都含有该方法。

### List
包含ArrayList和LinkedList两种：
+ ArrayList：长于随机访问元素，但中间插入和删除元素较慢
+ LinkedList：插入和删除元素较快，优化了顺序访问，但是随机访问比较慢
LinkedList实现Queue接口，另外我们也可以用它的特性来实现栈的LIFO功能。

### 迭代器
*迭代器*是一个对象，它不必考虑底层结构即可遍历并选择序列中的对象。
主要方法有```Iterator()```,```next()```,```hasNext()```,```remove()```。

### Set
![](/images/posts/think_in_java/set.png)
TreeSet可分为字典、字母排序，需要传入参数

### Map
![](/images/posts/think_in_java/map.png)
常用的方法有```get()```,```put()```,```keySet()```,```values()```。