---
layout: post
title: "Windows下caffe环境搭建"
date: 2018-6-6
description: "Windows下caffe环境搭建"
tag: 深度学习
---  

近期由于课程设计需要用到caffe框架，就尝试了Windows环境配置caffe环境，谁知这是一个大坑啊，各种问题解决起来花个两三天是正常的。本人大部分按照下面的教程进行https://blog.csdn.net/maltliquor/article/details/78261339 和 https://blog.csdn.net/maltliquor/article/details/78284141 ，并记录一些自己遇到的奇特的坑。这两个教程是连续的，后面一个在caffe安装成功后配置python环境。

### 关于软件版本
caffe需要用visual studio编译，需要注意的是caffe需要VS2013和VS2015才能编译，caffe2需要VS2015和VS2017编译。
caffe使用的python版本是2.x，推荐使用Anaconda，注意Anaconda2对接python2，Anaconda3对接python3，一开始就试过下载Anaconda3然后出问题了。。另外下载的时候也要和系统位数相同的，64位系统理论上能兼容32位，但需要额外的配置才能运行。如果电脑中已经有python先查看是否位数相同，推荐使用Anaconda内置的python。像我直接使用32位python会报一下错误
```
error LNK2001: 无法解析的外部符号
```
对于CUDA caffe支持8.0，建议下载8.0版本和cudnn5.0，注意各个软件的兼容。
关于caffe编译前的附件包含目录，教程里需要进行配置，实践中发现不配置也能编译成功