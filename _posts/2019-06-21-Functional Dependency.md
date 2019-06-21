---
layout: post
title: Functional Dependency
subtitle: MySQL学习笔记系列
date: 2019-06-21
author: Jalever
header-img: img/home-bg-geek.jpg
catalog: true
tags:
  - DBMS
---
## Overview

A functional dependency (FD) is a relationship between two attributes, typically between the PK and other non-key attributes within a table. For any relation R, attribute Y is functionally dependent on attribute X (usually the PK), if for every valid instance of X, that value of X uniquely determines the value of Y. This relationship is indicated by the representation below :

![VzpGLD.png](https://s2.ax1x.com/2019/06/21/VzpGLD.png)

The left side of the above FD diagram is called the `determinant`, and the right side is the `dependent`.

Here are a few examples.

In the first example, below, SIN determines Name, Address and Birthdate. Given SIN, we can determine any of the other attributes within the table.
[![Vzpgoj.md.png](https://s2.ax1x.com/2019/06/21/Vzpgoj.md.png)](https://imgchr.com/i/Vzpgoj)

For the second example, SIN and Course determine the date completed (DateCompleted). This must also work for a composite PK.

[![VzpRFs.md.png](https://s2.ax1x.com/2019/06/21/VzpRFs.md.png)](https://imgchr.com/i/VzpRFs)

The third example indicates that ISBN determines Title.

[![VzpWYn.md.png](https://s2.ax1x.com/2019/06/21/VzpWYn.md.png)](https://imgchr.com/i/VzpWYn)

#### Trivial Functional Dependency
X → Y is a non trivial functional dependencies when Y is not a subset of X.

X → Y is called completely non-trivial when X intersect Y is NULL.
Examples:

![Vzp4S0.png](https://s2.ax1x.com/2019/06/21/Vzp4S0.png)

#### Non Trivial Functional Dependencies
X → Y is a non trivial functional dependencies when Y is not a subset of X.

X → Y is called completely non-trivial when X intersect Y is NULL.
Examples:

![VzpIyT.png](https://s2.ax1x.com/2019/06/21/VzpIyT.png)

#### Semi Non Trivial Functional Dependencies
X → Y is called semi non-trivial when X intersect Y is not NULL.
Examples:

![VzpbTJ.png](https://s2.ax1x.com/2019/06/21/VzpbTJ.png)

## What does functionally dependent mean?
A function dependency A → B means for all instances of a particular value of A, there is the same value of B.

For example in the below table A → B is true, but B → A is not true as there are different values of A for B = 3.
```bash
A   B
------
1   3
2   3
4   0
1   3
4   0
```
