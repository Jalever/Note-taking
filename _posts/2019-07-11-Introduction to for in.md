---
layout: post
title: Introduction to for...in
subtitle: Web Development
date: 2019-07-11
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Web Development
---

- [Overview](#overview)
    - [Syntax](#syntax)
        - [Parameters](#parameters)
- [Description](#description)
    - [Deleted Added and Modified Properties](#deleted-added-and-modified-properties)
    - [Array Iteration and for...in](#array-iteration-and-forin)
    - [Iterating over own properties only](#iterating-over-own-properties-only)
- [Why use for...in](#why-use-forin)
- [Examples](#examples)

## Overview
The `for...in` statement iterates over all <strong>non-Symbol</strong>, <strong>enumerable propertie</strong>s of an object.
![Z2cnkd.png](https://s2.ax1x.com/2019/07/11/Z2cnkd.png)


#### Syntax
![Z2cBcV.png](https://s2.ax1x.com/2019/07/11/Z2cBcV.png)

###### Parameters
&nbsp;&nbsp;<strong>variable</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;A different property name is assigned to variable on each iteration.

&nbsp;&nbsp;<strong>object</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Object whose <strong>non-Symbol</strong> enumerable properties are iterated over.

## Description
A `for...in` loop only iterates over enumerable, non-Symbol properties. Objects created from built–in constructors like <strong>Array</strong> and <strong>Object</strong> have inherited non–enumerable properties from <strong>Object.prototype</strong> and <strong>String.prototype</strong>, such as <strong>String</strong>'s <strong>indexOf()</strong> method or <strong>Object</strong>'s <strong>toString()</strong> method. The loop will iterate over all enumerable properties of the object itself and those the object inherits from its constructor's prototype (properties closer to the object in the prototype chain override prototypes' properties).

#### Deleted Added and Modified Properties
A `for...in` loop iterates over the properties of an object in an arbitrary order.

If a property is modified in one iteration and then visited at a later time, its value in the loop is its value at that later time. A property that is deleted before it has been visited will not be visited later. Properties added to the object over which iteration is occurring may either be visited or omitted from iteration.

In general, it is best not to add, modify, or remove properties from the object during iteration, other than the property currently being visited. There is no guarantee whether an added property will be visited, whether a modified property (other than the current one) will be visited before or after it is modified, or whether a deleted property will be visited before it is deleted

#### Array Iteration and for...in
> `for...in` should not be used to iterate over an `Array` where the index order is important.

<strong>Array</strong> indexes are just enumerable properties with integer names and are otherwise identical to general object properties. There is no guarantee that `for...in` will return the indexes in any particular order. The `for...in` loop statement will return all enumerable properties, including those with non–integer names and those that are inherited.

Because the order of iteration is implementation-dependent, iterating over an array may not visit elements in a consistent order. Therefore, it is better to use a <strong>for</strong> loop with a numeric index (or <strong>Array.prototype.forEach()</strong> or the `for...of` loop) when iterating over arrays where the order of access is important.

#### Iterating over own properties only
If you only want to consider properties attached to the object itself, and not its prototypes, use <strong>getOwnPropertyNames()</strong> or perform a <strong>hasOwnProperty()</strong> check (<strong>propertyIsEnumerable()</strong> can also be used). Alternatively, if you know there won't be any outside code interference, you can extend built-in prototypes with a check method.

## Why use for...in
Given that `for...in` is built for iterating object properties, not recommended for use with arrays, and options like <strong>Array.prototype.forEach()</strong> and `for...of` exist, what might be the use of `for...in` at all?

It may be most practically used for debugging purposes, being an easy way to check the properties of an object (by outputting to the console or otherwise). Although arrays are often more practical for storing data, in situations where a key-value pair is preferred for working with data (with properties acting as the "key"), there may be instances where you want to check if any of those keys hold a particular value.

## Examples
The `for...in` loop below iterates over all of the object's enumerable, non-Symbol properties and logs a string of the property names and their values.
![Z2Rl11.png](https://s2.ax1x.com/2019/07/11/Z2Rl11.png)

The following function illustrates the use of <strong>hasOwnProperty()</strong>: the inherited properties are not displayed.
![Z2RY7D.png](https://s2.ax1x.com/2019/07/11/Z2RY7D.png)
