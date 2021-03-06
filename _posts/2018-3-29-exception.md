---
layout: post
title: "异常"
date: 2018-3-29
description: "通过异常处理错误"
tag: think in java 读书笔记 
---  

### 基本异常
异常情形是阻止当前方法求作用域继续执行的问题（区别于普通问题）
标准异常类的构造器包含有：
+ 默认构造器
+ 接收字符串做参数

### 捕获异常
监控区域——在try块里面
异常处理程序——catch块：就像一个接收且仅接收一个特殊类型的参数的方法。
对于出现异常的处理有两种模型：终止模型和恢复模型。终止模型即结束方法，恢复即企图恢复现场，这种想法很美好但是实际中实现难度大，所以一般的语言都选择终止模型。

### 创建自定义异常
创建异常，**类名**最重要，最好使用那种能一眼看出作用的名字。
打印时使用```System.err()```可发送给标准错误流，使用```System.out```可能会被重定向。
另外利用日志记录功能也可把异常发送给日志。

### 异常说明
属于方法声明的一部分，紧跟在形参列表之后。

### 捕获所有异常
使用异常基类Exception
抛出栈轨迹
重新抛出异常，构成异常链。

### java标准异常
Throwable
+ Error
+ Exception
RuntimeException

### finally
这个块总会被执行
当要把出内存块之外的资源恢复到初始状态时，就要用finally子句