---
layout: post
title: Object
subtitle: Javascript Standard Built-in Object
date: 2019-03-26
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - JavaScript
---

- [Properties](#properties)
    - [Object.prototype](#objectprototype)
    - [Object.prototype.constructor](#objectprototypeconstructor)
- [Methods](#methods)
    - [Object.assign()](#objectassign)
    - [Object.create()](#objectcreate)
    - [Object.defineProperties()](#objectdefineproperties)
    - [Object.defineProperty()](#objectdefineproperty)
    - [Object.entries()](#objectentries)
    - [Object.freeze()](#objectfreeze)
    - [Object.fromEntries()](#objectfromentries)
    - [Object.getOwnPropertyDescriptor()](#objectgetownpropertydescriptor)
    - [Object.getOwnPropertyDescriptors()](#objectgetownpropertydescriptors)
    - [Object.getOwnPropertyNames()](#objectgetownpropertynames)
    - [Object.getOwnPropertySymbols()](#objectgetownpropertysymbols)
    - [Object.getPrototypeOf()](#objectgetprototypeof)
    - [Object.is()](#objectis)
    - [Object.isExtensible()](#objectisextensible)
    - [Object.isFrozen()](#objectisfrozen)
    - [Object.isSealed()](#objectissealed)
    - [Object.keys()](#objectkeys)
    - [Object.preventExtensions()](#objectpreventextensions)
    - [Object.prototype.hasOwnProperty()](#objectprototypehasownproperty)
    - [Object.prototype.isPrototypeOf()](#objectprototypeisprototypeof)
    - [Object.prototype.propertyIsEnumerable()](#objectprototypepropertyisenumerable)
    - [Object.prototype.toLocaleString()](#objectprototypetolocalestring)
    - [Object.prototype.toString()](#objectprototypetostring)
    - [Object.prototype.valueOf()](#objectprototypevalueof)
    - [Object.seal()](#objectseal)
    - [Object.setPrototypeOf()](#objectsetprototypeof)
    - [Object.values()](#objectvalues)

## Properties

#### Object.prototype

#### Object.prototype.constructor

## Methods

#### Object.assign()

#### Object.create()

#### Object.defineProperties()

#### Object.defineProperty()

#### Object.entries()

#### Object.freeze()

#### Object.fromEntries()

#### Object.getOwnPropertyDescriptor()

#### Object.getOwnPropertyDescriptors()

#### Object.getOwnPropertyNames()

#### Object.getOwnPropertySymbols()

#### Object.getPrototypeOf()

#### Object.is()

###### Definition
The `Object.is()` method determines whether two values are the same value.
Two values are the same if one of the following holds:
- both `undefined`
- both `null`
- both `true` or both `false`
- both strings of the same length with the same characters in the same order
- both the same object
- both numbers and
  - both `+0`
  - both `-0`
  - both `NaN`
  - both non-zero and both not `NaN` and both ahve the same value

###### Syntax
![ZD4Cz8.png](https://s2.ax1x.com/2019/07/08/ZD4Cz8.png)

1.<strong>Parameters</strong>
- <strong>value1</strong>
    The first value to compare.
- <strong>value2</strong>
The second value to compare.

2.<strong>Return value</strong>
A `Boolean` indicating whether or not the two arguments are the same value.

###### Usage

```javascript
Object.is('foo', 'foo');     // true
Object.is(window, window);   // true

Object.is('foo', 'bar');     // false
Object.is([], []);           // false

var foo = { a: 1 };
var bar = { a: 1 };
Object.is(foo, foo);         // true
Object.is(foo, bar);         // false

Object.is(null, null);       // true

// Special Cases
Object.is(0, -0);            // false
Object.is(-0, -0);           // true
Object.is(NaN, 0/0);         // true
```

#### Object.isExtensible()

#### Object.isFrozen()

#### Object.isSealed()

#### Object.keys()

#### Object.preventExtensions()

#### Object.prototype.hasOwnProperty()

#### Object.prototype.isPrototypeOf()

#### Object.prototype.propertyIsEnumerable()

#### Object.prototype.toLocaleString()

#### Object.prototype.toString()

#### Object.prototype.valueOf()

#### Object.seal()

#### Object.setPrototypeOf()

#### Object.values()
