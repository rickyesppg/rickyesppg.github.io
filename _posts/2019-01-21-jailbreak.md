---
layout: post
title:  class-dump
date:   2019-01-21
excerpt: "解决class-dump导不全头文件问题。"
project: true
tag:
- blog
comments: true
---

使用class-dump有时不能导出全部头文件问题

1、在手机端安装Cydia插件classdump-dyld
2、连接手机后cycript -p xxx 连接app
3、导入插件 @import net.limneos.classdumpdyld;
4、classdumpdyld.dumpClass(SpringBoard);    // 导出指定类的头文件 结合reveal工具使用
@"Wrote file /tmp/SpringBoard.h"

classdumpdyld.dumpBundle([NSBundle mainBundle]);
@"Wrote all headers to /tmp/SpringBoard"

// Dump any bundle other than the main bundle 
classdumpdyld.dumpBundle([NSBundle bundleWithIdentifier:@"com.apple.UIKit"]);
@"Wrote all headers to /tmp/UIKit"

// Dump any image loaded in the process using any class name it contains
classdumpdyld.dumpBundleForClass(CallBarControllerModern);
@"Wrote all headers to /tmp/CallBar7"
