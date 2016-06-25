---
author: mageric
comments: true
date: 2015-03-12 13:52:12+00:00
layout: post
title: Max Points on a Line
categories:
- 算法
tags:
- 算法
---
给定一些二维平面上的点，求出其中共线点最多时的点个数：    
解法：采用**暴力枚举**，时间复杂度有`O（n^2）`，循环计算两点之间的斜率，构造一个哈希表来存储循环检查的情况，其中key为斜率，value就是共线点的个数。特殊处理：当出现斜率无限大，也就是两点的x轴相同而y轴不同时，记斜率**slope**为`std:numeric_limits<double>::infinity`，即无限大。   
代码：
{% highlight c %}
int maxPoints(vector<Point> &points) {
   if (points.size() < 3) return points.size();
   int result = 0;
   unordered_map<double, int> slope_count;
   for (int i = 0; i < points.size()-1; i++) {
      slope_count.clear();
      int samePointNum = 0; // 与i 重合的点
      int point_max = 1; // 和i 共线的最大点数
      for (int j = i + 1; j < points.size(); j++) {
        double slope; // 斜率
        if (points[i].x == points[j].x) {
            slope = std::numeric_limits<double>::infinity();
            if (points[i].y == points[j].y) {
                ++ samePointNum;
                continue;
              }
           }else {
              slope = 1.0 * (points[i].y - points[j].y) /(points[i].x - points[j].x);
           }
        int count = 0;
        if (slope_count.find(slope) != slope_count.end())
            count = ++slope_count[slope];
        else {
            count = 2;
            slope_count[slope] = 2;
        }
        if (point_max < count) point_max = count;
     }     
    result = max(result, point_max + samePointNum);
  }  
  return result;
}
{% endhighlight %}
