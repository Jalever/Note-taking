---
layout: post
title: Introduction to for...of
subtitle: Statements and Declarations
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
- [Examples](#examples)
    - [Iterating over an Array](#iterating-over-an-array)
    - [Iterating over a String](#iterating-over-a-string)
    - [Iterating over a TypedArray](#iterating-over-a-typedArray)
    - [Iterating over a Map](#iterating-over-a-map)
    - [Iterating over a Set](#iterating-over-a-set)
    - [Iterating over the arguments object](#iterating-over-the-arguments-object)
    - [Iterating over a DOM collection](#iterating-over-a-dom-collection)
    - [Closing iterators](#closing-iterators)
    - [Iterating over generators](#iterating-over-generators)
        - [Do not reuse generators](#do-not-reuse-generators)
    - [Iterating over other iterable objects](#iterating-over-other-iterable-objects)

## Overview
The `for...of` statement creates a loop iterating over iterable objects, including: built-in <strong>String</strong>, <strong>Array</strong>, <strong>Array-like object</strong>s (e.g., <strong>arguments</strong> or <strong>NodeList</strong>), <strong>TypedArray</strong>, <strong>Map</strong>, <strong>Set</strong>, and user-defined iterables. It invokes a custom iteration hook with statements to be executed for the value of each distinct property of the object.
![Z2hah4.png](https://s2.ax1x.com/2019/07/11/Z2hah4.png)


#### Syntax
![Z2h4gA.png](https://s2.ax1x.com/2019/07/11/Z2h4gA.png)

###### Parameters
&nbsp;&nbsp;<strong>variable</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;On each iteration a value of a different property is assigned to variable. variable may be declared with <strong>const</strong>, <strong>let</strong>, or <strong>var</strong>.

&nbsp;&nbsp;<strong>iterable</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Object whose iterable properties are iterated.

## Examples

#### Iterating over an Array
![Z2IAXR.png](https://s2.ax1x.com/2019/07/11/Z2IAXR.png)

You can use `const` instead of `let` too, if you don't reassign the variable inside the block.
![Z2I03Q.png](https://s2.ax1x.com/2019/07/11/Z2I03Q.png)

#### Iterating over a String
![Z2oAPS.png](https://s2.ax1x.com/2019/07/11/Z2oAPS.png)

#### Iterating over a TypedArray
![Z2oZvj.png](https://s2.ax1x.com/2019/07/11/Z2oZvj.png)

#### Iterating over a Map
![Z2oMV0.png](https://s2.ax1x.com/2019/07/11/Z2oMV0.png)

#### Iterating over a Set
![Z2o3PU.png](https://s2.ax1x.com/2019/07/11/Z2o3PU.png)

#### Iterating over the arguments object
You can iterate over the <strong>arguments</strong> object to examine all of the parameters passed into a JavaScript function:
![Z2oIJS.png](https://s2.ax1x.com/2019/07/11/Z2oIJS.png)

#### Iterating over a DOM collection
Iterating over DOM collections like `NodeList`: the following example adds a `read` class to paragraphs that are direct descendants of an article:
![Z2ojoV.png](https://s2.ax1x.com/2019/07/11/Z2ojoV.png)

#### Closing iterators
In `for...of` loops, abrupt iteration termination can be caused by `break`, `throw` or `return`. In these cases, the iterator is closed.
![Z2TPy9.png](https://s2.ax1x.com/2019/07/11/Z2TPy9.png)

#### Iterating over generators
You can also iterate over <strong>generator</strong>s, i.e. functions generating an iterable object:
![Z2TJFf.png](https://s2.ax1x.com/2019/07/11/Z2TJFf.png)

#### Do not reuse generators
Generators should not be re-used, even if the `for...of` loop is terminated early, for example via the `break` keyword. Upon exiting a loop, the generator is closed and trying to iterate over it again does not yield any further results.
![Z2TBmn.png](https://s2.ax1x.com/2019/07/11/Z2TBmn.png)

#### Iterating over other iterable objects
You can also iterate over an object that explicitly implements the <strong>iterable</strong> protocol:
![Z2opDI.png](https://s2.ax1x.com/2019/07/11/Z2opDI.png)
