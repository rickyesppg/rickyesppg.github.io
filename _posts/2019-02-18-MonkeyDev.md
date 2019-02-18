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
 1、首先声明要想hook的类<br>
 CHDeclareClass(QADImageSplashViewController);<br>
 2、hook原来类的方法。<br>
 CHOptimizedMethod2(self, id, QADImageSplashViewController, initWithNibName, id, arg1, bundle, id, arg2) {<br>

    return nil;<br>
 }<br>
 
 //CHOptimizedMethod2(optimization, return_type, class_type, name1, type1, arg1, name2, type2, arg2)<br>
 optimization:一般返回self。<br>
 return_type:方法返回值。<br>
 class_type:hook的类。<br>
 name1:第一个方法名。<br>
 type1:第一个方法类型。<br>
 arg1:第一个参数。<br>
 name2:第二个方法名。<br>
 type2:第二个方法类型。<br>
 arg2:第二个参数。<br>
 3、构造函数(类和方法必须再这里声明)<br>
 CHConstructor {<br>
    CHLoadLateClass(QADImageSplashViewController);<br>
 
    CHHook2(QADImageSplashViewController, initWithNibName, bundle);<br>
 }<br>
 

 
 
