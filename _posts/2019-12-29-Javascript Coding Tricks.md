---
layout: post
title: Javascript Coding Tricks
subtitle: Javascript Coding Techniques
date: 2019-12-29
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Web Development
---

- [Double Bitwise NOT Shorthand](#double-bitwise-not-shorthand)
- [Exponent Power Shorthand](#exponent-power-shorthand)
- [Converting a String into a Number](#converting-a-string-into-a-number)

## Double Bitwise NOT Shorthand

Bitwise operators are one of those features you learn about in beginner JavaScript tutorials and you never get to implement them anywhere. Besides, who wants to work with ones and zeroes if you are not dealing with binary?

There is, however, a very practical use case for the Double Bitwise NOT operator. You can use it as a replacement for Math.floor(). The advantage of the Double Bitwise NOT operator is that it performs the same operation much faster.

Longhand:

```js
Math.floor(4.9) === 4; //true
```

Shorthand:

```js
~~4.9 === 4; //true
```

## Exponent Power Shorthand

Shorthand for a Math exponent power function:

Longhand:

```js
Math.pow(2, 3); // 8
Math.pow(2, 2); // 4
Math.pow(4, 3); // 64
```

Shorthand:

```js
2 ** 3; // 8
2 ** 4; // 4
4 ** 3; // 64
```

## Converting a String into a Number

There are times when your code receives data that comes in String format but needs to processed in Numerical format. It’s not a big deal, we can perform a quick conversion.

Longhand:

```js
const num1 = parseInt("100");
const num2 = parseFloat("100.01");
```

Shorthand:

```js
const num1 = +"100"; // converts to int data type
const num2 = +"100.01"; // converts to float data type
```
