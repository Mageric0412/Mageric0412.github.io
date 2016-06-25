---
author: mageric
comments: true
date: 2015-04-02 05:22:00+00:00
layout: post
title: Unity5关于android的打包
categories:
- Unity5
tags:
- unity5
---
**unity5**打包apk需要将安装SDK升级到**android sdk 5.0 api 21**。    
国内使用SDK Manager.exe更新不了，于是下载sdk包手动更新到**sdk 5.0**。    
下载下面几个包：     
[https://dl-ssl.google.com/android/repository/sources-21_r01.zip](https://dl-ssl.google.com/android/repository/sources-21_r01.zip)     
[https://dl-ssl.google.com/android/repository/build-tools_r21.1-windows.zip](https://dl-ssl.google.com/android/repository/build-tools_r21.1-windows.zip)     
[https://dl-ssl.google.com/android/repository/tools_r23.0.5-windows.zip](https://dl-ssl.google.com/android/repository/tools_r23.0.5-windows.zip)     
[https://dl-ssl.google.com/android/repository/platform-tools_r21-windows.zip](https://dl-ssl.google.com/android/repository/platform-tools_r21-windows.zip)     
[https://dl-ssl.google.com/android/repository/samples-20_r02.zip](https://dl-ssl.google.com/android/repository/samples-20_r02.zip)     
[https://dl-ssl.google.com/android/repository/support_r21.0.1.zip](https://dl-ssl.google.com/android/repository/support_r21.0.1.zip)     
使用**easygo**翻墙下载，配合迅雷速度很快。下载之后解压到android-sdk目录下，没有就新建，对应解压路径为：    
**android-21_r01.zip**    
`>>> E:\android-sdk\platforms\ (将解压后的文件夹名android-5.0 改为 android-21)`  
**sources-21_r01.zip**     
`>>> E:\android-sdk\sources\ (将解压后的文件夹名rec 改为 android-21)`     
**build-tools_r21.1-windows.zip**     
`>>> E:\android-sdk\build-tools\ (将解压后的文件夹名android-5.0 改为 android-21)`     
**tools_r23.0.5-windows.zip**     
`>>> E:\android-sdk\ (覆盖原来的tools文件夹)`    
**platform-tools_r21-windows.zip**    
`>>> E:\android-sdk\ (覆盖原来的platform-tools文件夹)`    
**samples-20_r02.zip**     
`>>> E:\android-sdk\samples\support_r21.0.1.zip`
