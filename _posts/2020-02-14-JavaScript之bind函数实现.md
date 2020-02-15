---
layout: post
title: JavaScript深入之bind函数实现
subtitle: JavaScript系列
date: 2020-02-14
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - JavaScript
---

> 声明: 本文参照冴羽大大的文章


- [介绍](#%e4%bb%8b%e7%bb%8d)
- [返回函数的模拟实现](#%e8%bf%94%e5%9b%9e%e5%87%bd%e6%95%b0%e7%9a%84%e6%a8%a1%e6%8b%9f%e5%ae%9e%e7%8e%b0)
- [传参的模拟实现](#%e4%bc%a0%e5%8f%82%e7%9a%84%e6%a8%a1%e6%8b%9f%e5%ae%9e%e7%8e%b0)
- [构造函数效果的模拟实现](#%e6%9e%84%e9%80%a0%e5%87%bd%e6%95%b0%e6%95%88%e6%9e%9c%e7%9a%84%e6%a8%a1%e6%8b%9f%e5%ae%9e%e7%8e%b0)
- [构造函数效果的优化实现](#%e6%9e%84%e9%80%a0%e5%87%bd%e6%95%b0%e6%95%88%e6%9e%9c%e7%9a%84%e4%bc%98%e5%8c%96%e5%ae%9e%e7%8e%b0)
- [可能会遇到的问题](#%e5%8f%af%e8%83%bd%e4%bc%9a%e9%81%87%e5%88%b0%e7%9a%84%e9%97%ae%e9%a2%98)
- [最终代码](#%e6%9c%80%e7%bb%88%e4%bb%a3%e7%a0%81)

## 介绍
`bind()` 方法会创建一个新函数。当这个新函数被调用时，`bind()` 的第一个参数将作为它运行时的 `this`，之后的一序列参数将会在传递的实参前传入作为它的参数

`bind`与`apply`和`call`的最大的区别是：`bind`不会立即调用，而是返回一个新函数，称为绑定函数，其内的`this`指向为创建它时传入`bind`的第一个参数，而传入`bind`的第二个及以后的参数作为原函数的参数来调用原函数

```js
const module = {
  x: 42,
  getX: function() {
    return this.x;
  }
}

const unboundGetX = module.getX;
console.log(unboundGetX()); // The function gets invoked at the global scope
// expected output: undefined

const boundGetX = unboundGetX.bind(module);
console.log(boundGetX());
// expected output: 42
```

由此我们可以首先得出 bind 函数的两个特点：

1. 返回一个函数
2. 可以传入参数

## 返回函数的模拟实现
从第一个特点开始，我们举个例子：
```js
var foo = {
    value: 1
};

function bar() {
    console.log(this.value);
}

// 返回了一个函数
var bindFoo = bar.bind(foo); 

bindFoo(); // 1
```

关于指定 this 的指向，我们可以使用 call 或者 apply 实现.我们来写第一版的代码：
```js
// 第一版
Function.prototype.bind2 = function (context) {
    var self = this;
    return function () {
        return self.apply(context);
    }
}
```

之所以 `return self.apply(context)`，是考虑到绑定函数可能是有返回值的，依然是这个例子：
```js
var foo = {
    value: 1
};

function bar() {
	return this.value;
}

var bindFoo = bar.bind(foo);

console.log(bindFoo()); // 1
```

## 传参的模拟实现
接下来看第二点，可以传入参数。在指向Function.prototype.bind时, 除了可以传参，还可以在返回的函数传参，参考一下例子:
```js
var foo = {
    value: 1
};

function bar(name, age) {
    console.log(this.value);
    console.log(name);
    console.log(age);
}

var bindFoo = bar.bind(foo, 'daisy');
bindFoo('18');
// 1
// daisy
// 18
```

代码实现:
```js
// 第二版
Function.prototype.bind2 = function (context) {

    var self = this;
    // 获取bind2函数从第二个参数到最后一个参数
    var args = Array.prototype.slice.call(arguments, 1);

    return function () {
        // 这个时候的arguments是指bind返回的函数传入的参数
        var bindArgs = Array.prototype.slice.call(arguments);
        return self.apply(context, args.concat(bindArgs));
    }
}
```

## 构造函数效果的模拟实现
`Function.prototype.bind`还有一个特点，就是:
> 一个绑定函数也能使用`new`操作符创建对象：这种行为就像把原函数当成构造器。提供的 `this` 值被忽略，同时调用时的参数被提供给模拟函数

也就是说当 `bind` 返回的函数作为构造函数的时候，`bind` 时指定的 `this` 值会失效，但传入的参数依然生效。举个例子：
```js
var value = 2;

var foo = {
    value: 1
};

function bar(name, age) {
    this.habit = 'shopping';
    console.log(this.value);
    console.log(name);
    console.log(age);
}

bar.prototype.friend = 'kevin';

var bindFoo = bar.bind(foo, 'daisy');

var obj = new bindFoo('18');
// undefined
// daisy
// 18
console.log(obj.habit);
console.log(obj.friend);
// shopping
// kevin
```

注意：尽管在全局和 `foo` 中都声明了 `value` 值，最后依然返回了 `undefind`，说明绑定的 `this` 失效了，如果大家了解 `new` 的模拟实现，就会知道这个时候的 `this` 已经指向了 `obj`

所以我们可以通过修改返回的函数的原型来实现，让我们写一下：
```js
// 第三版
Function.prototype.bind2 = function (context) {
    var self = this;
    var args = Array.prototype.slice.call(arguments, 1);

    var fBound = function () {
        var bindArgs = Array.prototype.slice.call(arguments);
        // 当作为构造函数时，this 指向实例，此时结果为 true，将绑定函数的 this 指向该实例，可以让实例获得来自绑定函数的值
        // 以上面的是 demo 为例，如果改成 `this instanceof fBound ? null : context`，实例只是一个空对象，将 null 改成 this ，实例会具有 habit 属性
        // 当作为普通函数时，this 指向 window，此时结果为 false，将绑定函数的 this 指向 context
        return self.apply(this instanceof fBound ? this : context, args.concat(bindArgs));
    }
    // 修改返回函数的 prototype 为绑定函数的 prototype，实例就可以继承绑定函数的原型中的值
    fBound.prototype = this.prototype;
    return fBound;
}
```

## 构造函数效果的优化实现
但是在这个写法中，我们直接将 `fBound.prototype = this.prototype`，我们直接修改 fBound.prototype 的时候，也会直接修改绑定函数的 prototype。这个时候，我们可以通过一个空函数来进行中转：
```js
// 第四版
Function.prototype.bind2 = function (context) {

    var self = this;
    var args = Array.prototype.slice.call(arguments, 1);

    var fNOP = function () {};

    var fBound = function () {
        var bindArgs = Array.prototype.slice.call(arguments);
        return self.apply(this instanceof fNOP ? this : context, args.concat(bindArgs));
    }

    fNOP.prototype = this.prototype;
    fBound.prototype = new fNOP();
    return fBound;
}
```

## 可能会遇到的问题

1. 调用 bind 的不是函数咋办？
不行，我们要报错！
```js
if (typeof this !== "function") {
  throw new Error("Function.prototype.bind - what is trying to be bound is not callable");
}
```

## 最终代码
所以最最后的代码就是：
```js
Function.prototype.bind2 = function (context) {

    if (typeof this !== "function") {
      throw new Error("Function.prototype.bind - what is trying to be bound is not callable");
    }

    var self = this;
    var args = Array.prototype.slice.call(arguments, 1);

    var fNOP = function () {};

    var fBound = function () {
        var bindArgs = Array.prototype.slice.call(arguments);
        return self.apply(this instanceof fNOP ? this : context, args.concat(bindArgs));
    }

    fNOP.prototype = this.prototype;
    fBound.prototype = new fNOP();
    return fBound;
}
```
