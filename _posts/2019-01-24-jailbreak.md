---
layout: post
title:  重签名打包
date:   2019-01-24
excerpt: "使用ldid、codesign等工具重签名app。"
project: true
tag:
- blog
comments: true
---
<center>打包签名</center><br>
0、使用otool -l xxx.app/xxx | grep crypt   0为砸壳 1未砸壳 <br>

1、tweak打包后的包在.theos/obj/debug/xxx.dylib  <br>
2、使用otool -L xxx.dylib查看包依赖   <br>
3、install_name_tool -change /Library/Frameworks/CydiaSubstrate.framework/CydiaSubstrate @loader_path/libsubstrate.dylib xxx.dylib<br>
4、将xxx.dylib libsubstrate.dylib 放入xxx.app中 然后使用 optool install -c load -p "@executable_path/xxx.dylib" -t  /xxx.app/xxx  (libsubstrate.dylib该文件应该在/opt/thoes/lib/目录下)<br>
5、对xxx.lib和libsubstrate.dylib 签名 codesign -f -s "iPhone Developer: xxx (xxx)"  xxx.dylib<br>
6、对xxx.app中Frameworks所有的lib进行签名  codesign -f -s "iPhone Developer: xxx (xxx)" xxx.framework 注意是所有<br>
7、生成的plist文件放入xxx.app中。plist可以使用ldid -e xxx来生成<br>
8、使用iOS App Siner工具签名<br>

—查看mac上的证书<br>
# 查看当前系统中可用的所有签名证书 <br>
security find-identity -v -p codesigning   <br>
# 签名, 可以加 -f 参数 以覆盖签名 <br>
codesign -s 'iPhone Developer: xxx (5TPNQN7D6K)' Example.app<br>
# 查看签名状态 <br>
codesign -vv -d Example.app <br>
