---
layout: post
title: Memoize Function
subtitle: Web Development学习笔记系列
date: 2019-06-02
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Web Development
---
```js
function memoize(fn) {
    return function () {
        var args =
Array.prototype.slice.call(arguments)
        fn.cache = fn.cache || {};
        return fn.cache[args] ? fn.cache[args] : (fn.cache[args] = fn.apply(this,args))
    }
}
```
