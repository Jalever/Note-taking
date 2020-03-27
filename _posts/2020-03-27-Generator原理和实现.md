---
layout: post
title: Generator原理和实现
subtitle: JavaScript原理和实现系列
date: 2020-03-27
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - JavaScript
---

## 原理
`Generator` 实现的核心在于上下文的保存, 函数并没有真的被挂起，每一次 `yield`, 其实都执行了一遍传入的生成器函数, 只是在这个过程中间用了一个 `context` 对象储存上下文, 使得每次执行生成器函数的时候, 都可以从上一个执行结果开始执行, 看起来就像函数被挂起了一样

## 低配实现
```js
function genSwitch(_context) {
  while (1) {
    switch (_context.prev = _context.next) {
      case 0:
        _context.next = 2;
        return 'result1';

      case 2:
        _context.next = 4;
        return 'result2';

      case 4:
        _context.next = 6;
        return 'result3';

      case 6:
      default:
        return _context.stop();
    }
  }
}

const context = {
  prev: 0,
  next: 0,
  done: false,
  stop: function () {
    this.done = true;
  }
};

const gen = function () {
  return {
    next: function () {
      let value = context.done ? undefined : genSwitch(context);
      let done = context.done;

      console.warn('value');
      console.log(value);
      console.log('\n');

      return {
        value,
        done
      }
    }
  }
}

let g = gen();
g.next();
g.next();
g.next();

//output:
// result1
// result2
// result3

```




