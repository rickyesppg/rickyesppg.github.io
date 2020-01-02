---
layout: post
title: mobileconfig 签名
date:   2017-12-13
excerpt: "mobileconfig 签名"
project: true
tag:
- blog
comments: true
---
 
    
<center>
<b> mobileconfig 签名</b><br>

</center>
 
1、从服务器下载ssl证书<br>
2、找到Apache文件中3个文件。openssl smime -sign -in demo.mobileconfig -out signed.mobileconfig -signer demo.crt -inkey demo.key -certfile 1_root_bundle.crt -outform der -nodetach

 

 
 

 
 
 
