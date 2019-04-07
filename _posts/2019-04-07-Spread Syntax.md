---
layout: post
title: Spread Syntax
subtitle: 原生JavaScript学习笔记系列
date: 2019-04-07
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - JavaScript
  - Plain JavaScript
---

## Definition
`Spread syntax` allows an iterable such as an `array expression` or `string` to be expanded in places where zero or more arguments (for function calls) or elements (for array literals) are expected, or `an object` expression to be expanded in places where zero or more key-value pairs (for object literals) are expected.

## Syntax
For function calls:
```javascript
myFunction(...iterableObj);
```
For `array literals` or `strings`:
```javascript
[...iterableObj, '4', 'five', 6];
```
For `object literals`
```javascript
let objClone = { ...obj };
```
