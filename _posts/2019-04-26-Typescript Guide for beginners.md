---
layout: post
title: Typescript Guide for beginners
subtitle: Learn TypeScript in 30 Minutes
date: 2019-04-26
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Typescript
---
- [The Benefits of Using TypeScript](#the-benefits-of-using-typeScript)
- [Static Typing](#static-typing)
- [Interfaces](#interfaces)
- [Classes](#classes)
- [Generics](#generics)

## The Benefits of Using TypeScript
JavaScript is pretty good as it is and you may wonder Do I really need to learn TypeScript? Technically, you do not need to learn TypeScript to be a good developer, most people do just fine without it. However, working with TypeScript definitely has its benefits:
- Due to the static typing, code written in TypeScript is more predictable, and is generally easier to debug.
- Makes it easier to organize the code base for very large and complicated apps thanks to modules, namespaces and strong OOP support.
- TypeScript has a compilation step to JavaScript that catches all kinds of errors before they reach runtime and break something.

## Static Typing
A very distinctive feature of TypeScript is the support of static typing. This means that you can declare the types of variables, and the compiler will make sure that they aren't assigned the wrong types of values. If type declarations are omitted, they will be inferred automatically from your code.

Here is an example. Any variable, function argument or return value can have its type defined on initialization:
![eGGmxH.png](https://s2.ax1x.com/2019/07/30/eGGmxH.png)
Because TypeScript is compiled to JavaScript, and the latter has no idea what types are, they are completely removed:
![eGGKsA.png](https://s2.ax1x.com/2019/07/30/eGGKsA.png)
However, if we try to do something illegal, on compilation `tsc` will warn us that there is an error in our code. For example:
![eGGGi8.png](https://s2.ax1x.com/2019/07/30/eGGGi8.png)
![eGGyJU.png](https://s2.ax1x.com/2019/07/30/eGGyJU.png)
It will also warn us if we pass the wrong argument to a function:
![eGGWLR.png](https://s2.ax1x.com/2019/07/30/eGGWLR.png)
![eGGTJO.png](https://s2.ax1x.com/2019/07/30/eGGTJO.png)
Here are some of the most commonly used data types:
- <strong>Number</strong>&minus;All numeric values are represented by the number type, there aren't separate definitions for integers, floats or others.
- <strong>String</strong>&minus;The text type, just like in vanilla JS strings can be surrounded by 'single quotes' or "double quotes".
- <strong>Boolean</strong>&minus;`true` or `false`, using 0 and 1 will cause a compilation error.
- <strong>Any</strong>&minus;A variable with this type can have it's value set to a string, number, or anything else.
- <strong>Arrays</strong>&minus;Has two possible syntaxes: `my_arr: number[];` or `my_arr: Array<number>`.
- <strong>Void</strong>&minus;Used on function that don't return anything.

## Interfaces
Interfaces are used to type-check whether an object fits a certain structure. By defining an interface we can name a specific combination of variables, making sure that they will always go together. When translated to JavaScript, interfaces disappear - their only purpose is to help in the development stage.

In the below example we define a simple interface to type-check a function's arguments:
![eGYw5V.png](https://s2.ax1x.com/2019/07/30/eGYw5V.png)
The order of the properties does NOT matter. We just need the required properties to be present and to be the right type. If something is missing, has the wrong type, or is named differently, the compiler will warn us.
![eGYRV1.png](https://s2.ax1x.com/2019/07/30/eGYRV1.png)
![eGYf56.png](https://s2.ax1x.com/2019/07/30/eGYf56.png)

## Classes
When building large scale apps, the object oriented style of programming is preferred by many developers, most notably in languages such as Java or C#. TypeScript offers a class system that is very similar to the one in these languages, including inheritance, abstract classes, interface implementations, setters/getters, and more.

It's also fair to mention that since the most recent JavaScript update (ECMAScript 2015), classes are native to vanilla JS and can be used without TypeScript. The two implementation are very similar but have their differences, TypeScript being a bit more strict.

Continuing with the food theme, here is a simple TypeScript class:
![eGRq58.png](https://s2.ax1x.com/2019/07/30/eGRq58.png)
![eGROPS.png](https://s2.ax1x.com/2019/07/30/eGROPS.png)
Anyone who has written at least a bit of Java or C# should find this syntax comfortably familiar. The same goes for inheritance:
![eGWmrR.png](https://s2.ax1x.com/2019/07/30/eGWmrR.png)
![eGWKVx.png](https://s2.ax1x.com/2019/07/30/eGWKVx.png)

## Generics
Generics are templates that allow the same function to accept arguments of various different types. Creating reusable components using generics is better than using the any data type, as generics preserve the types of the variables that go in and out of them.

A quick example would be a script that receives an argument and returns an array containing that same argument.
![eGWNqI.png](https://s2.ax1x.com/2019/07/30/eGWNqI.png)
The first time we called the function we manually set the type to string. This isn't required as the compiler can see what argument has been passed and automatically decide what type suits it best, like in the second call. Although it's not mandatory, providing the type every time is considered good practice as the compiler might fail to guess the right type in more complex scenarios.
