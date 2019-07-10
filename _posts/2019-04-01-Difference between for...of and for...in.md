---
layout: post
title: Difference between for...of and for...in
subtitle: Web Development
date: 2019-04-01
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Web Development
---
- [for...of](#forof)
- [for...in](#forin)

Both `for...in` and `for...of` statements iterate over something.<br>
The main difference between them is in what they iterate over.<br>

## for...of
Use `for…of` to iterate over the values in an <strong>iterable</strong>, like an <ins>Array</ins> for example:
![ZctbGj.png](https://s2.ax1x.com/2019/07/10/ZctbGj.png)

<ins>String</ins>s are also an iterable type, so you can use `for…of` on strings:
![ZcNiW9.png](https://s2.ax1x.com/2019/07/10/ZcNiW9.png)

You can also iterate over <ins>map</ins>s, <ins>set</ins>s, <ins>generator</ins>s, <ins>DOM node collection</ins>s and the <ins>arguments object</ins> available inside a functions.

## for...in
The `for...in` statement iterates over all <strong>non-Symbol</strong>, <strong>enumerable properties</strong> of an object.

Use `for…in` to iterate over the properties of an <ins>Object</ins> (the object keys):
![ZcNBSs.png](https://s2.ax1x.com/2019/07/10/ZcNBSs.png)

You can also use `for…in` to iterate over the index values of an iterable like an <ins>Array</ins> or a <ins>String</ins>:
![ZcN6mV.png](https://s2.ax1x.com/2019/07/10/ZcN6mV.png)
