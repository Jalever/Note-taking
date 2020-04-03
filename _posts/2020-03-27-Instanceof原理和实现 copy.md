---
layout: post
title: Instanceof原理和实现
subtitle: JavaScript原理和实现系列
date: 2020-03-27
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - JavaScript
---

## 定义和使用
`instanceof` 是用来判断 `A` 是否为 `B` 的实例，表达式为：`A instanceof B`，如果 `A` 是 `B` 的实例，则返回 `true`,否则返回 `false`

```js
var arr = new Array();
console.log(arr instanceof Array); //true
console.log(arr instanceof Object) //true,因为Array是object的子类
function test(){};
var testInstance = new test();
console.log(testInstance instanceof test); //true
```

## 原理
`left` 的 `__proto__` 是不是等于 `right.prototype`, 不等于时就再找 `left.__proto__.__proto__`, 一直找到 `__proto__` 为 `null`


## 实现
![GPzrwT.png](https://s1.ax1x.com/2020/03/27/GPzrwT.png)
```js
function instance_of(left, right) {
  let leftValue = left._proto_;
  let rightPrototype = right.prototype;

  while (true) {
    if (leftValue === null) return false;
    if (leftValue === rightPrototype) return true;
    leftValue = leftValue._proto_;
  }
}
```



