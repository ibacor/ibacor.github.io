---
layout: post
title: "初始化与清理"
date: 2018-3-6
description: "java的初始化"
tag: think in java 读书笔记 
---  

​    

​    要深入学习java，了解初始化和清理过程时必不可少的。

### 构造器
构造器是一个特殊的方法，它名字与类名相同，没有返回值（不同于void），可以含参数列表（没有任何参数则为默认构造器，如果你的类没有构造器，则编译器会自动创建一个默认构造器）。使用new语句则调用构造器，会为对象分配存储空间。
### 方法重载
在前面我们看到，几个构造器名字相同，为了解决名字相同造成的冲突问题，java引入了一种叫*方法重载*的机制。
所谓重载，即**在一个类里面，方法名字相同而参数不同，返回类型、修饰符可同可不同**。所以，对于重载方法，由于它们名字相同，唯一的区分标准就是**形参列表**。那么为什么不能以返回值区分呢（修饰符只起修饰作用）？原因就是当我们不需要返回值只是单纯调用方法执行某种操作时，编译器就不知道该调用哪种方法来。例如
```
void f(){}
int f(){return 1;}
```
调用``` f()```  
另外，当调用重载方法时，若传入的参数类型小于形参，则会自动转换类型；若传入实参较大，就需要类型转换来窄化转换。

### this关键字
this关键字只能在方法中使用，表示对“调用方法的那个对象”的引用。常用于return或把当前对象传递给其他方法。另外在构造器中使用this也可表示调用其他构造器。还有一种用法就是若方法参数s和类的数据成员名字相同，也可用this.s区分开来。

### static的补充
利用this，可从另外一个角度解读static：
+  static方法就是没有this的方法（因为没有对象）；
+  在static的内部不能调用非静态方法。

### 清理：终结处理和垃圾回收
要深入理解清理需要学习jvm，限于知识的缺乏目前只能先记一点知识点。
关于垃圾回收，有三点需要注意：
+  对象可能不被垃圾回收；
+  垃圾回收并不等于C++的“析构”；
+  垃圾回收只与内存有关
并且jvm在未面临内存耗尽时不会进行垃圾回收。
在java 中有一个finalize()方法，当垃圾回收器准备回收对象时首先调用finalize ()方法，并在**下一次**垃圾回收时真正回收对象的内存。

### 成员初始化
java尽力保证每个变量使用前都被初始化。其中，类的每个基本类型数据成员都有一个初始值（默认值），对于对象则为null。

### 构造器初始化
关于初始化的顺序，**类中数据成员会先自动初始化，然后构造器初始化**。
对于静态数据的初始化，则是先**初始化静态对象（且只初始化一次），然后初始化非静态对象**。另外在java中有一个叫*静态子句*的东西，它把多个静态初始化动作组织在一起，如下
```
static int i;
static double d;
static{
    i = 1;
    d = 2.2;
}
```
这样的静态子句也会被执行，且只被执行一次。
如果去掉static就叫*非静态初始化子句*，它可被执行多次且在构造器前执行。

### 数组初始化
数组在java中会自动检查边界，避免不可控行为的发生，付出的代价是效率降低。
可以使用new在数组里创建元素，但不能创建单个基本类型数据。
有时候我们会看到有这样的代码
```
static void fun(Object... args){
    //
}
```
这其实是可变参数列表，可以看作数组的推广，这样在调用该方法的时候就可以传入多个该类型的参数。但是这样遇到重载就会出现问题，所以只能在重载方法的一个版本上使用可变参数列表或者不用！