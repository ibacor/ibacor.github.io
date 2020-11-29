---
layout: post
title: "解释器模式"
date: 2020-1-21
description: "解释器模式"
tag: 设计模式
---  

解释器模式维护比较繁杂，一般在项目中很少遇到。
#### 定义
> 给定一门语言，定义它的文法的一种表示，并定义一个解释器，该解释器使用该表示来解释语言中的句子。

通用类图如下：  
![](/images/posts/designpattern/interpreter.png)  
类图中AbstractExpression是TerminalExpression和NonterminalExpression的抽象。  TerminalExpression即终结符表达式，实现与文法中元素相关联的解释操作，一般只会有一个终结符表达式。  
NonterminalExpression即非终结符表达式，文法中每条规则对应一个非终结符表达式，原则上每个文法规则对应一个非终结符表达式。

#### 优点
- 拓展性强，如果要拓展语法直接增加非终结符类即可

#### 缺点
- 容易导致类膨胀
- 采用了递归条用，调试复杂，效率低

#### 使用场景
- 重复发生的问题
- 简单的语法解释场景

#### 注意事项
项目中尽量避免使用解释器模式，推荐使用脚本语言或者成熟商业工具

参考：
> 设计模式之禅