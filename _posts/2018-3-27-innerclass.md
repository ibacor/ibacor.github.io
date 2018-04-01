---
layout: post
title: "内部类"
date: 2018-3-27
description: "内部类"
tag: think in java 读书笔记 
---  
   所谓**内部类**，就是把一个类的定义放在另一个类的定义内部。
### 创建内部类
创建内部类的方式很简单，只需在一个类里面进行定义即可，并且也可能是public的。如果在外部类的。如果想从外部类的非静态方法之外的任意位置创建某个内部类的对象，需要具体指明：OuterClassName.InnerClassName。

### 链接到外部类
使用内部类可以做到名字隐藏和组织代码，此外内部类还能与外部类拥有联系，它拥有对外部类所有元素的访问权。这个怎么做到的呢？事实上当某个外部类的对象创建一个内部类的时候，这个内部类对象会秘密捕获一个指向外部类对象的引用，也就是说，内部类的对象只能在与外部类的对象相关联的情况下才能被创建。

### 使用.this和.new
如果需要生成对外部类的引用，可以使用外部类的名字后面紧跟.this。需要创建内部类对象时需要先创建外部类对象并利用这个外部类对象来创建。
```
public class DotThis{
    class Inner{
        public DotThis outer(){ return DotThis.this; }
    }
}

public stastic void main(String[] args){
    DotThis dt = new DotThis();
    DotThis.Inner dti = dt.new Inner();
}
```

### 在方法和作用域内的内部类
这样的内部类的作用有两个：
1. 实现某个接口并返回该类型的引用
2. 想创建一个类但又不希望它是公开的

### 匿名内部类
这是一种看起来比较奇怪又很常见语法形式。
比如：
```
public class Parcel7{
    public Contents contents(){
        return new Contents(){
            private int i = 21;
            public int value(){ return i; }
        };
    }
}
```
可以看到，return那个语句是返回一个content对象，但是在结束前（分好前面）又插入了一个类的定义。实际上这种奇怪的语法指的是：“**创建一个继承自Contents的匿名类的对象**”，匿名的意思就是没有名字，上述代码可以看出是下述形式的简化形式：
```
public class Parcel7b{
    class MyContents implements Contents{
        private int i = 11;
        public int value(){ return i; }
    }
    public Contents contents(){ return new MyContents; }
}
```
若要在匿名内部类中使用外部参数，需要把这个参数设为final类型。并且由于它没有名字，也就意味着没有构造器，可以使用*实例初始化*达到构造器的效果。
使用匿名内部类有一些限制，它能继承类也能实现接口，但只能实现一种。

### 嵌套类
把内部类声明为static，即为*嵌套类*，此时**内部类对象不再与外部类对象有联系**，也就是说此时创建内部类对象不再需要外部类对象，而且内部类对象也不能访问非静态外部类对象。
在普通内部类中不能有static数据和static字段，也不能有嵌套类，但是嵌套类可以。
从多层嵌套类中也可以方位外部类的成员，不过嵌套了多少层。

### 为什么需要内部类
其实如果外部类实现接口能够满足需求，那么就不需要内部类去完成。
同时因为每个内部类都能独立继承一个接口实现，可达到“多重继承”的效果。