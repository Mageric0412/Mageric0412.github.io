---
author: mageric
comments: true
date: 2015-06-12 11:47:33+00:00
layout: post
title: DirectX 11 SDK的一些问题
wordpress_id: 230
categories:
- 图形学
tags:
- DX
---
由于项目需要，学习英伟达的**D3D11**新技术Sample。在一个使用**fx**渲染器的案例中，提示    
`unrecognized complier target " fx_5_0"`,网上搜索后得知，该`fx_5_0`新特性必须使用最新的**SDK11**才能编译。    
最后通过`fxc.exe`的命令支持发现，只有**DirectX SDK (June)2010**才提供`fx_5_0`的编译需求。    
所以推荐使用**D3D11**较新技术的时候，都将**DX SDK**更新到**（June）2010**版本（大概500多MB的），同时认真读取每份Sample的使用文档来设置环境，一劳永逸，切勿胡乱尝试。    
**这是教训所谈**。
