---
author: mageric
comments: true
date: 2015-03-19 13:46:14+00:00
layout: post
title: Hamming Weight在计算数中二进制1个数的应用
categories:
- 算法
tags:
- 位运算
---
代码：    
{% highlight c %}
  //types and constants used in the functions below
  typedef unsigned __int64 uint64; //assume this gives 64-bits
  const uint64 m1 = 0x5555555555555555; //binary: 0101...
  const uint64 m2 = 0x3333333333333333; //binary: 00110011..
  const uint64 m4 = 0x0f0f0f0f0f0f0f0f; //binary: 4 zeros, 4 ones ...
  const uint64 m8 = 0x00ff00ff00ff00ff; //binary: 8 zeros, 8 ones ...
  const uint64 m16 = 0x0000ffff0000ffff; //binary: 16 zeros, 16 ones ...
  const uint64 m32 = 0x00000000ffffffff; //binary: 32 zeros, 32 ones
  const uint64 hff = 0xffffffffffffffff; //binary: all ones
  const uint64 h01 = 0x0101010101010101; //the sum of 256 to the power of 0,1,2,3...
  //This is a naive implementation, shown for comparison,
  //and to help in understanding the better functions.
  //It uses 24 arithmetic operations (shift, add, and).
int popcount_1(uint64 x) {
    x = (x & m1 ) + ((x >> 1) & m1 ); //put count of each 2 bits into those 2 bits
    x = (x & m2 ) + ((x >> 2) & m2 ); //put count of each 4 bits into those 4 bits
    x = (x & m4 ) + ((x >> 4) & m4 ); //put count of each 8 bits into those 8 bits
    x = (x & m8 ) + ((x >> 8) & m8 ); //put count of each 16 bits into those 16 bits
    x = (x & m16) + ((x >> 16) & m16); //put count of each 32 bits into those 32 bits
    x = (x & m32) + ((x >> 32) & m32); //put count of each 64 bits into those 64 bits
    return x;
}
{% endhighlight %}
原理：   
**第一步**：计算一个数n位的奇偶位上的1的总和表示：m1就是0101 ,收集在偶数位上的1的情况，与奇数位上的情况进行相加，即收集每两位奇偶位。这样，原本n位的数位情况变成n/2位，相当于每两位代表对应奇偶数位上的1的个数，比如0110代表第一组奇偶位上有1个1，第二组奇偶位上有2（二进制10）个1；   
**第二步**：同第一步的思路，将每四位奇偶位上的1进行收集，利用1100、0011进行位计算。收集到的新数字每单元有4位，代表每4位的奇偶位上的1的二进制数目     
.........    
以此类推，每次收集位数的叠加数量分别为2、4、8、16、32，一般计算机整型表示为32位，那么迭代到32这一组就可以结束。    
**优点**：32位的数字最多只需要迭代5次，相比位与运算最多需要32次要更快。    
**缺点**：理解有难点，难以快速编写。
