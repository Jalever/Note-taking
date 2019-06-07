---
layout: post
title: Singleton Pattern
subtitle: Design Pattern学习笔记系列
date: 2019-06-07
author: Jalever
header-img: img/home_bg_tree.png
catalog: true
tags:
  - Design Pattern
---
The singleton pattern is a design pattern that restricts the instantiation of a class to one object.

The first time getInstance() is called it creates a new singleton object and after that it just returns the same object.

Note that Singleton obj is not created until we need it and call getInstance() method.

```java
// Classical Java implementation of singleton  
// design pattern
class Singleton
{
    private static Singleton obj;

    // private constructor to force use of
    // getInstance() to create Singleton object
    private Singleton() {}

    public static Singleton getInstance()
    {
        if (obj==null)
            obj = new Singleton();
        return obj;
    }
}
```
