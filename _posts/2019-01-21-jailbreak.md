---
layout: post
title:  class-dump
date:   2019-01-21
excerpt: "解决class-dump导不全头文件问题。"
 
tag:
- blog
comments: true
---

使用class-dump有时不能导出全部头文件问题<br>  

1、在手机端安装Cydia插件classdump-dyld<br>
2、连接手机后cycript -p xxx 连接app<br>
3、导入插件 @import net.limneos.classdumpdyld;<br>
4、classdumpdyld.dumpClass(SpringBoard);    // 导出指定类的头文件 结合reveal工具使用<br>
@"Wrote file /tmp/SpringBoard.h"<br>

classdumpdyld.dumpBundle([NSBundle mainBundle]);<br>
@"Wrote all headers to /tmp/SpringBoard"<br>

// Dump any bundle other than the main bundle <br>
classdumpdyld.dumpBundle([NSBundle bundleWithIdentifier:@"com.apple.UIKit"]);<br>
@"Wrote all headers to /tmp/UIKit"<br>

// Dump any image loaded in the process using any class name it contains<br>
classdumpdyld.dumpBundleForClass(CallBarControllerModern);<br>
@"Wrote all headers to /tmp/CallBar7"<br>
