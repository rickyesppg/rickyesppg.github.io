---
layout: post
title:  腾讯视频逆向
date:   2019-01-28
excerpt: "腾讯视频逆向。"
 
tag:
- blog
comments: true
---
<center>流程</center><br>
1、砸壳。先用frida-ios-dump砸壳。<br>
越狱手机ssh连接，在mac端命令行输入dump.py -l来查看砸壳应用。<br>
确定应用名称后，使用dump.py 腾讯视频，或者dump.py com.tencent.live4iphone命令来砸壳。<br>

2、得到头文件。<br>
将腾讯视频.ipa文件解压，进入腾讯视频.app同级目录，在mac端命令行使用class-dump -H live4iphone.app/live4iphone -o liveheads目录方法头文件<br>

3、分析开屏广告<br>
使用Reveal工具(第一次使用需要在设置>Reveal>Enabled Application中启用对应的腾讯视频app)查看开屏广告的控制器或者相应view的信息。<br>
经reveal查看后，得知控制器是QADImageSplashViewController，从头文件中找到对应的方法。<br>

QADImageSplashViewController可能没有从class-dump中导出来，需要使用classdump-dyld工具。 <br>
ssh连接iphone后用
*ps -e
*cycript -p live4iphone 
*@import net.limneos.classdumpdyld
*classdumpdyld.dumpClass(QADImageSplashViewController)
*找到文件/var/mobile/Containers/Data/Application/4FE862A1-FA06-4B9E-BDBF-8A0C8F9A70D3/Documents/QADImageSplashViewController.h，可以用pp助手将其拖放到mac文件夹liveheads
尝试hook

4、tweak
nic.pl新建一个tweak项目,hook该类的-(id)initWithNibName:(id)arg1 bundle:(id)arg2方法。可以看到没有开屏广告了，但会有一闪而过。我们再分析可能是动画或者其他引起的。但当前类中貌似没有相应方法，我们去父类中看看。









QADImageSplashViewController   0x1570f2a70

QADSplashContainerView    0x1570490c0


