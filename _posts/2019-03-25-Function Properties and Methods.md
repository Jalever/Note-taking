---
layout: post
title: Function Properties and Methods
subtitle: Javascript Standard Built-in Object
date: 2019-03-25
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - JavaScript
---

- [Overview](#overview)
- [Syntax](#syntax)
    - [Parameters](#parameters)
- [Properties and Methods of Function](#properties-and-methods-of-function)
    - [Properties of the Function prototype object](#properties-of-the-function-prototype-object)
        - [Function.prototype.length](#functionprototypelength)
        - [Function.prototype.name](#functionprototypename)
        - [Function.prototype.constructor](#functionprototypeconstructor)
    - [Methods of the Function prototype object](#methods-of-the-function-prototype-object)
        - [Function.prototype.apply()](#functionprototypeapply)
        - [Function.prototype.bind()](#functionprototypebind)
        - [Function.prototype.constructor](#functionprototypecall)
        - [Function.prototype.toString()](#functionprototypetostring)

## Overview
The `Function` <strong>constructor</strong> creates a new `Function` <strong>object</strong>. Calling the constructor directly can create functions dynamically, but suffers from security and similar (but far less significant) performance issues to `eval`. However, unlike eval, the Function constructor creates functions which execute in the global scope only.
![eUicBF.png](https://s2.ax1x.com/2019/08/01/eUicBF.png)
Every JavaScript function is actually a `Function` object. This can be seen with the code `(function(){}).constructor === Function` which returns true.

## Syntax
![eUiONd.png](https://s2.ax1x.com/2019/08/01/eUiONd.png)

#### Parameters
&nbsp;&nbsp;&nbsp;&nbsp;<strong>arg1, arg2, ... argN</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Names to be used by the function as formal argument names. Each must be a string that corresponds to a valid JavaScript identifier or a list of such strings separated with a comma; for example &quot;<strong>x</strong>&quot;, &quot;<strong>theValue</strong>&quot;, or &quot;<strong>a,b</strong>&quot;.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>functionBody</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;A string containing the JavaScript statements comprising the function definition.<br/>

## Description
`Function` objects created with the `Function` constructor are parsed when the function is created. This is less efficient than declaring a function with a Function Expression or Function Statement and calling it within your code because such functions are parsed with the rest of the code.
![eUAbHU.png](https://s2.ax1x.com/2019/08/01/eUAbHU.png)

All arguments passed to the function are treated as the names of the identifiers of the parameters in the function to be created, in the order in which they are passed. Omitting an argument will result in the value of that parameter being `undefined`.

Invoking the `Function` constructor as a function (without using the new operator) has the same effect as invoking it as a constructor.

## Properties and Methods of Function
The global `Function` object has no methods or properties of its own. However, since it is a function itself, it does inherit some methods and properties through the prototype chain from `Function.prototype`.

#### Properties of the Function prototype object
###### Function.prototype.length
###### Function.prototype.name
###### Function.prototype.constructor

#### Methods of the Function prototype object
###### Function.prototype.apply()
The `apply()` method calls a function with a given `this` value, and `arguments` provided as an array (or an `array-like object`).
> array-like object
> - nodelist
> - arguments

> While the syntax of this function is almost identical to that of `call()`, the fundamental difference is that `call()` accepts an <strong>argument list</strong>, while `apply()` accepts a <strong>single array of arguments</strong>.

> When the first argument is undefined or null a similar outcome can be achieved using the array `spread syntax`.

![eUAvC9.png](https://s2.ax1x.com/2019/08/01/eUAvC9.png)

<strong>Syntax</strong><br/>
![eUEA4H.png](https://s2.ax1x.com/2019/08/01/eUEA4H.png)

&nbsp;&nbsp;<strong>Parameters</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>thisArg</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The value of `this` provided for the call to `func`. Note that `this` may not be the actual value seen by the method: if the method is a function in non-strict mode code, `null` and `undefined` will be replaced with the global object, and primitive values will be boxed. This argument is not optional.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>argsArray</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional. An array-like object, specifying the arguments with which `func` should be called, or `null` or `undefined` if no arguments should be provided to the function. Starting with ECMAScript 5 these arguments can be a generic array-like object instead of an array.<br/>
&nbsp;&nbsp;<strong>Return value</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;The result of calling the function with the specified `this` value and arguments.<br/>

<strong>Description</strong><br/>
You can assign a different `this` object when calling an existing function. `this` refers to the current object, the calling object. With `apply`, you can write a method once and then inherit it in another object, without having to rewrite the method for the new object.

`apply` is very similar to `call()`, except for the type of arguments it supports. You use an arguments array instead of a list of arguments (parameters). With `apply`, you can also use an array literal, for example, `func.apply(this, ['eat', 'bananas'])`, or an `Array` object, for example, `func.apply(this, new Array('eat', 'bananas'))`.

You can also use `arguments` for the `argsArray` parameter. `arguments` is a local variable of a function. It can be used for all unspecified arguments of the called object. Thus, you do not have to know the arguments of the called object when you use the `apply` method. You can use `arguments` to pass all the arguments to the called object. The called object is then responsible for handling the arguments.

Since ECMAScript 5th Edition you can also use any kind of object which is array-like, so in practice, this means it's going to have a property `length` and integer properties in the range `(0..length-1)`. As an example you can now use a `NodeList` or a custom object like `{ 'length': 2, '0': 'eat', '1': 'bananas' }`.

<strong>Examples</strong><br/>
1.Using apply to append an array to another<br/>
We can use push to append an element to an array. And, because push accepts a variable number of arguments, we can also push multiple elements at once. But, if we pass an array to push, it will actually add that array as a single element, instead of adding the elements individually, so we end up with an array inside an array. What if that is not what we want? concat does have the behaviour we want in this case, but it does not actually append to the existing array but creates and returns a new array. But we wanted to append to our existing array... So what now? Write a loop? Surely not?

apply to the rescue!
![eUmFsI.png](https://s2.ax1x.com/2019/08/01/eUmFsI.png)

2.Using apply and built-in functions<br/>
Clever usage of `apply` allows you to use built-in functions for some tasks, that otherwise probably would have been written by looping over the array values. As an example here we are going to use `Math.max`/`Math.min`, to find out the maximum/minimum value in an array.
![eUmZo8.png](https://s2.ax1x.com/2019/08/01/eUmZo8.png)
But beware: in using `apply` this way, you run the risk of exceeding the JavaScript engine's argument length limit. The consequences of applying a function with too many arguments (think more than tens of thousands of arguments) vary across engines (JavaScriptCore has hard-coded argument limit of 65536), because the limit (indeed even the nature of any excessively-large-stack behavior) is unspecified. Some engines will throw an exception. More perniciously, others will arbitrarily limit the number of arguments actually passed to the applied function. To illustrate this latter case: if such an engine had a limit of four arguments (actual limits are of course significantly higher), it would be as if the arguments `5, 6, 2, 3` had been passed to `apply` in the examples above, rather than the full array.

If your value array might grow into the tens of thousands, use a hybrid strategy: apply your function to chunks of the array at a time:
![eUmNYF.png](https://s2.ax1x.com/2019/08/01/eUmNYF.png)

3.Using apply to chain constructors<br/>
You can use `apply` to chain constructors for an object, similar to Java. In the following example we will create a global `Function` method called `construct`, which will enable you to use an array-like object with a constructor instead of an arguments list.
![eUmBO1.png](https://s2.ax1x.com/2019/08/01/eUmBO1.png)
Example usage:
![eUmgYD.png](https://s2.ax1x.com/2019/08/01/eUmgYD.png)

###### Function.prototype.bind()
###### Function.prototype.call()
###### Function.prototype.toString()
