---
layout: post
title: Async && Await原理和实现
subtitle: JavaScript原理和实现系列
date: 2020-03-27
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - JavaScript
---

- [async/await的使用](#asyncawait%e7%9a%84%e4%bd%bf%e7%94%a8)
- [generator的含义和使用](#generator%e7%9a%84%e5%90%ab%e4%b9%89%e5%92%8c%e4%bd%bf%e7%94%a8)
- [yield 和async/await 的不同](#yield-%e5%92%8casyncawait-%e7%9a%84%e4%b8%8d%e5%90%8c)
- [手写自执行Generator](#%e6%89%8b%e5%86%99%e8%87%aa%e6%89%a7%e8%a1%8cgenerator)
- [函数实现基础版](#%e5%87%bd%e6%95%b0%e5%ae%9e%e7%8e%b0%e5%9f%ba%e7%a1%80%e7%89%88)
- [函数实现加强版](#%e5%87%bd%e6%95%b0%e5%ae%9e%e7%8e%b0%e5%8a%a0%e5%bc%ba%e7%89%88)

## async/await的使用
async/await 实际上是对 Generator（生成器）的封装，是一个语法糖.


```js
async () => {
  const a = awaitPromise.resolve(a);
  const b = awaitPromise.resolve(b);
  const c = awaitPromise.resolve(c);
}
```

## generator的含义和使用
`ES6`新引入了 `Generator` 函数，可以通过 `yield` 关键字，把函数的执行流挂起，通过 `next()`方法可以切换到下一个状态，为改变执行流程提供了可能，从而为异步编程提供解决方案

```js
function* myGenerator() {
  yield'1'
  yield'2'
  return'3'
}

const gen = myGenerator();  // 获取迭代器
gen.next();  
//{value: "1", done: false}

gen.next();  
//{value: "2", done: false}

gen.next();  
//{value: "3", done: true}
```

也可以通过给`next()`传参, 让 `yield` 具有返回值
```js
function* myGenerator() {
  console.log(yield '1')  
  console.log(yield '2')  
  console.log(yield '3')  
}

// 获取迭代器
const gen = myGenerator();

gen.next()
gen.next('test1')
gen.next('test2')
gen.next('test3')

//test1
//test2
//test3
```

## yield 和async/await 的不同
虽然`yield`和`async/await`都提供了暂停执行的功能，但二者又有三点不同

- `async/await`自带执行器，不需要手动调用 `next()`就能自动执行下一步
- `async`函数返回值是 `Promise` 对象，而 `Generator` 返回的是生成器对象
- `await`能够返回 `Promise` 的 `resolve/reject` 的值


##  手写自执行Generator
```js
function* myGenerator() {
  yield Promise.resolve(1);
  yield Promise.resolve(2);
  yield Promise.resolve(3);
}

const gen = myGenerator();
gen.next().value.then(val => {
  console.log(val);
  gen.next().value.then(val => {
    console.log(val);
    gen.next().value.then(val => {
      console.log(val);
    })
  })
})

//输出1 2 3
```
我们也可以通过给gen.next()传值的方式，让 yield 能返回 resolve 的值
```js
function* myGenerator() {
  console.log(yield Promise.resolve(1))   //1
  console.log(yield Promise.resolve(2))   //2
  console.log(yield Promise.resolve(3))   //3
}

const gen = myGenerator();
gen.next().value.then(val1 => {
  gen.next(val1).value.then(val2 => {
    gen.next(val2).value.then(val3 => {
      gen.next(val3)
    })
  })
})
```

## 函数实现基础版
```js
function run(gen) {
    let g = gen();

    function step(yieldObj) {
        let nextYieldObj = g.next(yieldObj);

        if(nextYieldObj.done) return nextYieldObj.value;
        
        nextYieldObj.value.then(v => step(v));
    }

    step();
}
```

使用:
```js
function* mygenerator() {
  try {
    console.log(yield Promise.resolve(111));
    console.log(yield Promise.resolve(222));
    console.log(yield Promise.resolve(333));
  } catch (error) {
    console.log(error);
  }
}

// 111
// 222
// 333
```

## 函数实现加强版
虽然我们实现了 `Generator` 的自动执行以及让 `yield` 返回 `resolve` 的值，但上边的代码还存在着几点问题:

1. 需要兼容基本类型：这段代码能自动执行的前提是`yield`后面跟 `Promise`，为了兼容后面跟着基本类型值的情况，我们需要把 `yield` 跟的内容`(gen().next.value)`都用`Promise.resolve()`转化一遍
2. 缺少错误处理：上边代码里的 `Promise` 如果执行失败，就会导致后续执行直接中断，我们需要通过调用`Generator.prototype.throw()`，把错误抛出来，才能被外层的 `try-catch` 捕获到
3. 返回值是 `Promise`: `async/await`的返回值是一个 `Promise`,我们这里也需要保持一致，给返回值包一个 `Promise`


```js
function run(gen) {
  let g = gen();

  return new Promise((resolve, reject) => {
    function step(yieldObj) {
      let nextYieldObj;
      try {
        nextYieldObj = g.next(yieldObj);
      } catch (error) {
        reject(error);
      }

      if(nextYieldObj.done) resolve(nextYieldObj.value);

      Promise.resolve(nextYieldObj.value).then(v => {
        step(v);
      }, reason => {
        g.throw(reason);
      });
    }
    
    step();
  });
}

run(mygenerator);
```

