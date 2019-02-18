---
layout: post
title:  MonkeyDev
date:   2019-02-18
excerpt: "MonkeyDev的使用。"
project: true
tag:
- blog
comments: true
---
<center>MonkeyDev</center><br>
 1、首先声明要想hook的类
 CHDeclareClass(QADImageSplashViewController);
 2、hook原来类的方法。
 CHOptimizedMethod2(self, id, QADImageSplashViewController, initWithNibName, id, arg1, bundle, id, arg2) {

 return nil;
 }
 
 //CHOptimizedMethod2(optimization, return_type, class_type, name1, type1, arg1, name2, type2, arg2)
 optimization:一般返回self。
 return_type:方法返回值。
 class_type:hook的类。
 name1:第一个方法名。
 type1:第一个方法类型。
 arg1:第一个参数。
 name2:第二个方法名。
 type2:第二个方法类型。
 arg2:第二个参数。
 3、构造函数(类和方法必须再这里声明)
 CHConstructor {
 CHLoadLateClass(QADImageSplashViewController);
 
 CHHook2(QADImageSplashViewController, initWithNibName, bundle);
 }
 

 
 
