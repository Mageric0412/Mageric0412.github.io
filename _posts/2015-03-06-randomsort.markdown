---
author: mageric
comments: true
date: 2015-03-06 14:47:49+00:00
layout: post
title: 随机数组排序
categories:
- 算法
tags:
- 排序
---
如题，对一个数组进行**随机排序**，或者随机完整**输出数组中所有元素且不重复**：   
{% highlight c %}
int nTemp;
int nData[10], nTran[10];
for(i=0; i<10; i++)
   nTran[i]=i;
for(i=0; i<10; i++)
  {
   nTemp	= rand()%(10-i);
   nData[i]	= nTran[nTemp];
   nTran[nTemp]	= nTran[9-i];
  }
//printf(nData);
{% endhighlight %}
