---
layout: post
title: Basic Types
subtitle: Typescript学习笔记系列
date: 2019-05-31
author: Jalever
header-img: img/post_2019_react_contextAPI_bg.png
catalog: true
tags:
  - Typescript
---

## Basic Types
#### boolean

#### string

#### number

#### array
- []
```js
let list: number[] = [1, 2, 3];
```

- Array<elementType>
```js
let list: Array<number> = [1, 2, 3];
```

#### tuple
Expressing an array where the type of a fixed number of elements is known, but need not be the same.
```js
// Declare a tuple type
let x: [string, number];
// Initialize it
x = ["hello", 10]; // OK
// Initialize it incorrectly
x = [10, "hello"]; // Error
```

#### enum
```js
enum Color {Red = 1, Green, Blue}
let c: Color = Color.Green;
```

#### any

#### void

#### null and undefined

#### never
`never` is the return type for a function expression or an arrow function expression that always throws an exception or one that never returns;

#### object

## Type Assertions
Usually this will happen when you know the type of some entity could be more specific than its current type.
- angle-bracket
```js
let someValue: any = "this is a string";

let strLength: number = (<string>someValue).length;
```

- as-syntax
```js
let someValue: any = "this is a string";

let strLength: number = (someValue as string).length;
```
