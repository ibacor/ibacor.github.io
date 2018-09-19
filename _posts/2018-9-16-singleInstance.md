---
layout: post
title: "单例模式"
date: 2018-9-16
description: "单例模式的常见实现"
tag: 设计模式
---  

**单例模式**，顾名思义，就是这个类只能有一个实例，生命周期一般与应用相同，作用域一般是全局。单例模式是23中设计模式里面最简单的一个，本身也比较常见，所以了解它也是学习编程的基本要求。

**应用：**计数器、打印机对象、I/O流和socket等

#### 实现
##### 1.懒汉式（线程不安全）
这是最基本的单例模式，很简单，但是在多线程情况下可能会创建超过一个实例
```
public class Singleton {  
    private static Singleton instance;  
    private Singleton (){}
    public static Singleton getInstance() {
    if (instance == null) {	//这里有可能当一个线程执行下一条语句时又有另一个线程跑进来，从而创建两个实例
        instance = new Singleton();
    }
    return instance;
    }
}
```

##### 2.懒汉式（线程安全）
```
public class Singleton {
    private static Singleton instance;
    private Singleton (){}
    public static synchronized Singleton getInstance() {
    if (instance == null) {
        instance = new Singleton();
    }
    return instance;
    }
}
```
这种方式因为加了锁，所以能够避免第一种情况的缺点，但是方法加锁使得执行效率大大降低

##### 3.饿汉式
```
public class Singleton {
    private static Singleton instance = new Singleton();
    private Singleton (){}
    public static Singleton getInstance() {
    return instance;
    }
}
```
一般使用这种方式。饿汉式直接在类初始化时创建实例，避免多线程同步问题，同时效率也不会降低，缺点是可能有垃圾对象

##### 4.双重校验锁（double-checked locking）
```
public class Singleton {  
    private volatile static Singleton singleton;  
    private Singleton (){}
    public static Singleton getSingleton() {
    if (singleton == null) {
        synchronized (Singleton.class) {
        if (singleton == null) {
            singleton = new Singleton();
        }
        }
    }
    return singleton;
    }
}
```
这种实现起来比较复杂，看起来是懒汉式线程安全和线程不安全版本的结合体，也的确继承了它们的优点——既线程安全也能保证效率。

当遇到特殊需求无法用前三种方式实现时不妨尝试一下这种。