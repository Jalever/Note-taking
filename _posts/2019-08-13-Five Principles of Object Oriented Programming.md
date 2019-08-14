---
layout: post
title: Five Principles of Object Oriented Programming
subtitle: Web Development
date: 2019-08-13
author: Jalever
header-img: img/post_2019_web_development_bg.png
catalog: true
tags:
    - Web Development
---

## Overview
<strong>S.O.L.I.D</strong> is an acronym for the <strong>first five object-oriented design(OOD)</strong> principles by <ins>Robert C. Martin</ins>, popularly known as Uncle Bob.

These principles, when combined together, make it easy for a programmer to develop software that are easy to maintain and extend. They also make it easy for developers to avoid code smells, easily refactor code, and are also a part of the agile or adaptive software development.

S.O.L.I.D stands for:

When expanded the acronyms might seem complicated, but they are pretty simple to grasp.

- <strong>S</strong> - Single-responsiblity principle
- <strong>O</strong> - Open-closed principle
- <strong>L</strong> - Liskov substitution principle
- <strong>I</strong> - Interface segregation principle
- <strong>D</strong> - Dependency Inversion Principle

## Single-responsibility Principle


## Open-closed Principle


## Liskov substitution principle
#### Definition
Substitutability is a principle in Object-Oriented Programming stating that, in a Computer Program, if `S` is a subtype of `T`, then objects of type `T` may be replaced with objects of type `S` (i.e. an object of type `T` may be substituted with any object of a subtype `S`) without altering any of the desirable properties of the program (correctness, task performed, etc.).



## Interface segregation principle
#### Definition
A client should never be forced to implement an interface that it doesn't use or clients shouldn't be forced to depend on methods they do not use.

#### Example
Still using our shapes example, we know that we also have solid shapes, so since we would also want to calculate the volume of the shape, we can add another contract to the <strong>ShapeInterface</strong>:
![m9LtgI.png](https://s2.ax1x.com/2019/08/13/m9LtgI.png)
Any shape we create must implement the <strong>volume</strong> method, but we know that squares are flat shapes and that they do not have volumes, so this interface would force the <strong>Square</strong> class to implement a method that it has no use of.

<strong>ISP</strong> says no to this, instead you could create another interface called <strong>SolidShapeInterface</strong> that has the <strong>volume</strong> contract and solid shapes like cubes e.t.c can implement this interface:
![m9L84H.png](https://s2.ax1x.com/2019/08/13/m9L84H.png)
This is a much better approach, but a pitfall to watch out for is when type-hinting these interfaces, instead of using a <strong>ShapeInterface</strong> or a <strong>SolidShapeInterface</strong>.

You can create another interface, maybe <strong>ManageShapeInterface</strong>, and implement it on both the flat and solid shapes, this way you can easily see that it has a single API for managing the shapes. For example:
![m9LZC9.png](https://s2.ax1x.com/2019/08/13/m9LZC9.png)
Now in <strong>AreaCalculator</strong> class, we can easily replace the call to the <strong>area</strong> method with <strong>calculate</strong> and also check if the object is an instance of the <strong>ManageShapeInterface</strong> and not the <strong>ShapeInterface</strong>.

## Dependency Inversion principle
#### Definition
Entities must depend on abstractions not on concretions. It states that the high level module must not depend on the low level module, but they should depend on abstractions.
