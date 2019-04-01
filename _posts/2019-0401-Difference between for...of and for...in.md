---
layout: post
title: Difference between for...of and for...in
subtitle: Web Development学习笔记系列
date: 2019-04-01
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Web Development
---


Both `for...in` and `for...of` statements iterate over something. 
The main difference between them is in what they iterate over.

The `for...in` statement iterates over the <ins>***enumerable properties***</ins> of an object, in an arbitrary order.
> `enumerable properties`: A property is identified as enumerable or not by its own `[[Enumerable]]` attribute
> `for-in` 方法来遍历所有非 `Symbol` 类型并且是可枚举的属性

The `for...of` statement iterates over values that the <ins>***iterable object***</ins> defines to be iterated over.

The following example shows the difference between a `for...of` loop and a `for...in` loop when used with an `Array`.

```javascript
Object.prototype.objCustom = function() {}; 
Array.prototype.arrCustom = function() {};

let iterable = [3, 5, 7,32,333,432];
iterable.foo = 'hello';

for (let i in iterable) {
  console.log(i); 
  // logs 3, 5, 7, 32, 333, 432, "foo", "arrCustom", "objCustom"
}


for (let i of iterable) {
  console.log(i); // logs 3, 5, 7, 32, 333, 432
}
```
