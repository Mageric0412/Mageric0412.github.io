---
author: mageric
comments: true
date: 2015-04-09 15:33:00+00:00
layout: post
title: unity5中[Serializable]关键字
categories:
- Unity5
tags:
- unity5
---

![](http://7xvk1t.com1.z0.glb.clouddn.com/image/games/serializable.jpg)
Unity5中脚本C#有关键字`[Serializable]`,从C#的角度讲就是能够对所定义的类进行序列化，经过序列化的对象，可以暂时保存在硬盘上，而不占用内存，等到需要使用时再从硬盘读入。    
而Unity5中的`[Serializable]`接口声明的作用，就是能够将所定义的类在编辑器中实例展现出来。换而言之，就是能够通过在编辑器中设置，从而实例化该类。     
如图所示,官方案例`roguelike`中对`foodcount`和`wallcount`的实现就是通过在脚本中定义`[Serializable]`接口的**count**类,从而可以在编辑器界面上对该类进行实例化修改等。
{% highlight c# %}
[Serializable]
public class Count
{
  public int minimum;
  public int maximum;
  public Count (int min, int max)
 {
   minimum = min;
   maximum = max;
 }
}
..............
public Count wallCount = new Count (5, 9);
public Count foodCount = new Count (1, 5);
{% endhighlight %}
