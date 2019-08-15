---
layout: post
title: Arrow Function
subtitle: Javascript Functions
date: 2019-03-27
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - JavaScript
---

- [Overview](#overview)
- [Syntax](#syntax)
    - [Basic Syntax](#basic-syntax)
    - [Advanced Syntax](#advanced-syntax)
- [Description](#description)
    - [Shorter functions](#shorter-functions)
    - [No separate this](#no-separate-this)
        - [Relation with strict mode](#relation-with-strict-mode)
        - [Invoked through call or apply](#invoked-through-call-or-apply)
    - [No binding of arguments](#no-binding-of-arguments)
    - [Arrow functions used as methods](#arrow-functions-used-as-methods)
    - [Use of the new operator](#use-of-the-new-operator)
    - [Use of prototype property](#use-of-prototype-property)
    - [Use of the yield keyword](#use-of-the-yield-keyword)
- [Function Body](#function-body)
- [Returning object literals](#returning-object-literals)
- [Line breaks](#line-breaks)
- [Parsing order](#parsing-order)
- [More Examples](#more-examples)

## Overview
An <strong>arrow function expression</strong> is a syntactically compact alternative to a regular function expression, although without its own bindings to the `this`, `arguments`, `super`, or `new.target` keywords. Arrow function expressions are ill suited as methods, and they cannot be used as constructors.
![ZvxEeP.png](https://s2.ax1x.com/2019/07/19/ZvxEeP.png)

## Syntax
#### Basic Syntax
![Zvzp7V.png](https://s2.ax1x.com/2019/07/19/Zvzp7V.png)

#### Advanced Syntax
![ZvzPtU.png](https://s2.ax1x.com/2019/07/19/ZvzPtU.png)

## Description
Two factors influenced the introduction of arrow functions:
- the need for shorter functions
- the behavior of the this keyword

#### Shorter functions
![ZxSsPO.png](https://s2.ax1x.com/2019/07/19/ZxSsPO.png)
![ZxSyGD.png](https://s2.ax1x.com/2019/07/19/ZxSyGD.png)

#### No separate this
Before arrow functions, every new function defined its own <strong>this</strong> value based on how the function was called:
- A new object in the case of a constructor.
- <strong>undefined</strong> in `Strict Mode` function calls.
- The base object if the function was called as an "object method".
- etc.

This proved to be less than ideal with an object-oriented style of programming.
![ZxpiQJ.png](https://s2.ax1x.com/2019/07/19/ZxpiQJ.png)

In ECMAScript 3/5, the <strong>this</strong> issue was fixable by assigning the value in <strong>this</strong> to a variable that could be closed over.
![Zxplyd.png](https://s2.ax1x.com/2019/07/19/Zxplyd.png)

Alternatively, a bound function could be created so that a preassigned <strong>this</strong> value would be passed to the bound target function (the <strong>growUp()</strong> function in the example above).

An arrow function does not have its own <strong>this</strong>. <ins>The <strong>this</strong> value of the enclosing lexical scope is used</ins>; arrow functions follow the normal variable lookup rules. So while searching for this which is not present in current scope, an arrow function ends up finding the <strong>this</strong> from its enclosing scope.

Thus, in the following code, the <strong>this</strong> within the function that is passed to <strong>setInterval</strong> has the same value as the <strong>this</strong> in the lexically enclosing function:
![Zxp0yj.png](https://s2.ax1x.com/2019/07/19/Zxp0yj.png)

###### Relation with strict mode
Given that <strong>this</strong> comes from the surrounding lexical context, Strict Mode rules with regard to <strong>this</strong> are ignored.
![ZxCMqA.png](https://s2.ax1x.com/2019/07/19/ZxCMqA.png)

All other Strict Mode rules apply normally.

###### Invoked through call or apply
Since arrow functions do not have their own <strong>this</strong>, the methods <strong>call()</strong> and <strong>apply()</strong> can only pass in parameters. Any <strong>this</strong> argument is ignored.
![ZxCOLd.png](https://s2.ax1x.com/2019/07/19/ZxCOLd.png)

#### No binding of arguments
Arrow functions do not have their own <strong>arguments</strong> object. Thus, in this example, arguments is simply a reference to the <strong>arguments</strong> of the enclosing scope:
![ZxP2ff.png](https://s2.ax1x.com/2019/07/19/ZxP2ff.png)

In most cases, using Rest Parameters is a good alternative to using an <strong>arguments</strong> object.
![ZxP4XQ.png](https://s2.ax1x.com/2019/07/19/ZxP4XQ.png)

#### Arrow functions used as methods
As stated previously, arrow function expressions are best suited for non-method functions. Let's see what happens when we try to use them as methods:
![ZxidNq.png](https://s2.ax1x.com/2019/07/19/ZxidNq.png)

Arrow functions do not have their own <strong>this</strong>. Another example involving <strong>Object.defineProperty()</strong>:
![ZxiD3T.png](https://s2.ax1x.com/2019/07/19/ZxiD3T.png)

#### Use of the new operator
Arrow functions cannot be used as constructors and will throw an error when used with <strong>new</strong>.
![ZxiRER.png](https://s2.ax1x.com/2019/07/19/ZxiRER.png)

#### Use of prototype property
Arrow functions do not have a <strong>prototype</strong> property.
![ZxiIgO.png](https://s2.ax1x.com/2019/07/19/ZxiIgO.png)

#### Use of the yield keyword
The <strong>yield</strong> keyword may not be used in an arrow function's body (except when permitted within functions further nested within it). As a consequence, arrow functions cannot be used as generators.

## Function Body
Arrow functions can have either a "concise body" or the usual "block body".

In a concise body, only an expression is specified, which becomes the implicit return value. In a block body, you must use an explicit <strong>return</strong> statement.
![ZxFFVs.png](https://s2.ax1x.com/2019/07/19/ZxFFVs.png)

## Returning object literals
Keep in mind that returning object literals using the concise body syntax <strong>params => {object:literal}</strong> will not work as expected.
![ZxF2QS.png](https://s2.ax1x.com/2019/07/19/ZxF2QS.png)

This is because the code inside braces ({}) is parsed as a sequence of statements (i.e. <strong>foo</strong> is treated like a label, not a key in an object literal).

You must wrap the object literal in parentheses:
![ZxF4ds.png](https://s2.ax1x.com/2019/07/19/ZxF4ds.png)

## Line breaks
An arrow function cannot contain a line break between its parameters and its arrow.
![Zxk1Og.png](https://s2.ax1x.com/2019/07/19/Zxk1Og.png)

However, this can be amended by using parentheses or putting the line break inside the arguments as seen below to ensure that the code stays pretty and fluffy.
![ZxkGwj.png](https://s2.ax1x.com/2019/07/19/ZxkGwj.png)

## Parsing order
Although the arrow in an arrow function is not an operator, arrow functions have special parsing rules that interact differently with Operator Precedence compared to regular functions.
![ZxkwlT.png](https://s2.ax1x.com/2019/07/19/ZxkwlT.png)

## More Examples
![ZxAnHJ.png](https://s2.ax1x.com/2019/07/19/ZxAnHJ.png)
![ZxAQ41.png](https://s2.ax1x.com/2019/07/19/ZxAQ41.png)
![ZxA19x.png](https://s2.ax1x.com/2019/07/19/ZxA19x.png)
![ZxA336.png](https://s2.ax1x.com/2019/07/19/ZxA336.png)
![ZxA8gK.png](https://s2.ax1x.com/2019/07/19/ZxA8gK.png)
![ZxAGjO.png](https://s2.ax1x.com/2019/07/19/ZxAGjO.png)
