---
author: mageric
comments: true
date: 2015-07-02 13:26:20+00:00
layout: post
title: RTTI与typeid
categories:
- C++/C
tags:
- C++
---

**Typeid操作**返回指针或引用所指对象的实际类型。
如果一个基类中没有虚函数被实现，那么就算派生类中有同样的成员函数，指向派生类的指针的**Typeid**仍然是基类的类别；如果派生类重写了基类中虚函数，那么指向派生类的指针就是派生类的类。     
如有`class B`继承于`A`，`A* pA=new B()`;`typeid(pA)`就是`class *A`，`typeid(*pA)是指向**派生类的指针**，所以要**根据派生情况来RTTI他的类型**。
