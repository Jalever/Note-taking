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
- [for...of](#forof)
- [for...in](#forin)
- [Example](#example)

Both `for...in` and `for...of` statements iterate over something.<br>
The main difference between them is in what they iterate over.<br>
`数组`(或者`类数组对象`: `Strings`, `Maps`,`Sets`, `arguments`)的原型中都实现了一个方法 `Symbol.iterator`
`JavaScript` 虽然不支持用 `for-of` 来遍历`对象`，但是提供了一个 `for-in` 方法来遍历所有非 `Symbol` 类型并且是可枚举的属性

## for...of
The `for...of` statement iterates over values that the <ins>***iterable object***</ins> defines to be iterated over.<br>
you can get access to the array element itself<br>

## for...in
The `for...in` statement iterates over the <ins>***enumerable properties***</ins> of an object, in an arbitrary order.<br>
`for/in` looping constructs give you access to the index in the array, not the actual element.<br>
> `enumerable properties`: A property is identified as enumerable or not by its own `[[Enumerable]]` attribute<br>
> `for-in` 方法来遍历所有非 `Symbol` 类型并且是可枚举的属性<br>

## Example
The following example shows the difference between a `for...of` loop and a `for...in` loop when used with an `Array`.<br>

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
