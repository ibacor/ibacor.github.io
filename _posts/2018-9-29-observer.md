---
layout: post
title: "观察者模式"
date: 2018-9-29
description: "观察者模式"
tag: 设计模式
---  

观察者模式又叫发布订阅模式，有时候当一个对象状态发生改变时，我们希望能够自动通知相关的对象，这时候就用到*观察者模式*。

#### 应用场景
在一个目录新建一个文件时，自动通知目录管理器增加目录；
电视节目通过广播使电视机收到影像

#### 定义
定义对象间一种一对多的依赖关系，使得每当一个对象改变状态，则所有依赖于它的对象都会得到通知并自动更新。

UML图如下：
![]((/images/posts/designpattern/observer.png)
这个模型很简单，分为被观察者、观察者、具体的被观察者和具体的观察者，最终通过回调的方式通知观察者更新状态。

#### 实现
Subject类
```
import java.util.Vector;

public abstract class Subject {
    private Vector<Observer> list = new Vector<>();

    public void attach(Observer o){
        list.add(o);
    }

    public void detach(Observer o){
        list.remove(o);
    }

    public void notifyObservers(){
        for(Observer o : list){
            o.update();
        }
    }
}
```
ConcreteSubject类
```
public class ConcreteSubject extends Subject {
    public void doSomething(){
        //业务逻辑
    }
}
```

观察者
```
public interface Observer {
    void update();
}
```
具体的观察者
```
public class ConcreteObserver implements Observer {
    @Override
    public void update() {
        //业务逻辑
    }
}
```

#### 优点
- 观察者和被观察者是抽象耦合的
- 建立了一套触发机制

#### 缺点
- 如果观察者之间存在循环依赖，可能导致系统崩溃
- 没有相应机制知道所观察的目标对象是怎么发生变化的，而仅仅知道发生了变化

参考
> 设计模式之禅
> [观察者模式](http://www.runoob.com/design-pattern/observer-pattern.html)