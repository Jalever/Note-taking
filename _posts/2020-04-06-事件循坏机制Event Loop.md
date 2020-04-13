---
layout: post
title: 事件循坏机制Event Loop
subtitle: JavaScript深入学习系列
date: 2020-04-06
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - JavaScript
---
- [JavaScript语言的特点](#javascript%e8%af%ad%e8%a8%80%e7%9a%84%e7%89%b9%e7%82%b9)
- [浏览器环境下JavaScript引擎的事件循环机制](#%e6%b5%8f%e8%a7%88%e5%99%a8%e7%8e%af%e5%a2%83%e4%b8%8bjavascript%e5%bc%95%e6%93%8e%e7%9a%84%e4%ba%8b%e4%bb%b6%e5%be%aa%e7%8e%af%e6%9c%ba%e5%88%b6)
    - [执行栈与事件队列](#%e6%89%a7%e8%a1%8c%e6%a0%88%e4%b8%8e%e4%ba%8b%e4%bb%b6%e9%98%9f%e5%88%97)
    - [宏任务Macro Task与微任务Micro Task](#%e5%ae%8f%e4%bb%bb%e5%8a%a1macro-task%e4%b8%8e%e5%be%ae%e4%bb%bb%e5%8a%a1micro-task)
    - [例子](#%e4%be%8b%e5%ad%90)
- [node环境下的事件循环机制](#node%e7%8e%af%e5%a2%83%e4%b8%8b%e7%9a%84%e4%ba%8b%e4%bb%b6%e5%be%aa%e7%8e%af%e6%9c%ba%e5%88%b6)
- [参考链接](#%e5%8f%82%e8%80%83%e9%93%be%e6%8e%a5)



## JavaScript语言的特点
`JavaScript`是一门单线程的非阻塞的脚本语言。这是由其最初的用途来决定的：与浏览器交互。

单线程意味着, `JavaScript`代码在执行的任何时候，都只有一个主线程来处理所有的任务

而非阻塞则是当代码需要进行一项异步任务（无法立刻返回结果，需要花一定时间才能返回的任务，如I/O事件）的时候，主线程会挂起(pending)这个任务，然后在异步任务返回结果的时候再根据一定规则去执行相应的回调

单线程是必要的，也是`JavaScript`这门语言的基石，原因之一在其最初也是最主要的执行环境——浏览器中，我们需要进行各种各样的dom操作。试想一下 如果`JavaScript`是多线程的，那么当两个线程同时对dom进行一项操作，例如一个向其添加事件，而另一个删除了这个dom，此时该如何处理呢？因此，为了保证不会 发生类似于这个例子中的情景，`JavaScript`选择只用一个主线程来执行代码，这样就保证了程序执行的一致性

`JavaScript`的另一个特点是“非阻塞”，那么`JavaScript`引擎到底是如何实现的这一点呢？答案就是今天这篇文章的主角——Event Loop（事件循环）

## 浏览器环境下JavaScript引擎的事件循环机制

#### 执行栈与事件队列
当`JavaScript`代码执行的时候会将不同的变量存于内存中的不同位置：堆（heap）和栈（stack）中来加以区分。其中，堆里存放着一些对象。而栈中则存放着一些基础类型变量以及对象的指针

当我们调用一个方法的时候，js会生成一个与这个方法对应的执行环境（context），又叫`执行上下文`。这个执行环境中存在着这个方法的私有作用域，上层作用域的指向，方法的参数，这个作用域中定义的变量以及这个作用域的this对象。 而当一系列方法被依次调用的时候，因为js是单线程的，同一时间只能执行一个方法，于是这些方法被排队在一个单独的地方。这个地方被称为`执行栈`

当一个脚本第一次执行的时候，js引擎会解析这段代码，并将其中的同步代码按照执行顺序加入执行栈中，然后从头开始执行。如果当前执行的是一个方法，那么js会向执行栈中添加这个方法的执行环境，然后进入这个执行环境继续执行其中的代码。当这个执行环境中的代码 执行完毕并返回结果后，js会退出这个执行环境并把这个执行环境销毁，回到上一个方法的执行环境。这个过程反复进行，直到执行栈中的代码全部执行完毕

下图非常直观的展示了这个过程，其中的global就是初次运行脚本时向执行栈中加入的代码
![GyCq41.gif](https://s1.ax1x.com/2020/04/06/GyCq41.gif)

从图片可知，一个方法执行会向执行栈中加入这个方法的执行环境，在这个执行环境中还可以调用其他方法，甚至是自己，其结果不过是在执行栈中再添加一个执行环境。这个过程可以是无限进行下去的，除非发生了栈溢出，即超过了所能使用内存的最大值。

以上的过程说的都是同步代码的执行。那么当一个异步代码（如发送ajax请求数据）执行后会如何呢？前文提过，js的另一大特点是非阻塞，实现这一点的关键在于下面要说的这项机制——`事件队列`（Task Queue）。

js引擎遇到一个异步事件后并不会一直等待其返回结果，而是会将这个事件挂起，继续执行执行栈中的其他任务。当一个异步事件返回结果后，js会将这个事件加入与当前执行栈不同的另一个队列，我们称之为`事件队列`。被放入事件队列不会立刻执行其回调，而是等待当前执行栈中的所有任务都执行完毕， 主线程处于闲置状态时，主线程会去查找事件队列是否有任务。如果有，那么主线程会从中取出排在第一位的事件，并把这个事件对应的回调放入执行栈中，然后执行其中的同步代码...，如此反复，这样就形成了一个无限的循环。这就是这个过程被称为`事件循环(Event Loop)`的原因

这里还有一张图来展示这个过程:
![GyPPUA.png](https://s1.ax1x.com/2020/04/06/GyPPUA.png)
图中的`stack`表示我们所说的执行栈，`WebAPIs`则是代表一些异步事件，而`callback queue`即事件队列


#### 宏任务Macro Task与微任务Micro Task
以上的事件循环过程是一个宏观的表述，实际上因为异步任务之间并不相同，因此他们的执行优先级也有区别。不同的异步任务被分为两类：`微任务(Micro Task)`和`宏任务(Macro Task)`

以下事件属于微任务
- process.nextTick
- new Promise()
- Async/Await(实际就是promise)
- new MutaionObserver()

以下事件属于宏任务：
- script(整体代码)
- setInterval()
- setTimeout()
- setImmediate
- I/O
- UI rendering

前面我们介绍过，在一个事件循环中，异步事件返回结果后会被放到一个任务队列中。然而，根据这个异步事件的类型，这个事件实际上会被对应的<strong>宏任务队列</strong>或者<strong>微任务队列</strong>中去。并且在当前执行栈为空的时候，主线程会 查看<strong>微任务队列</strong>是否有事件存在。如果不存在，那么再去<strong>宏任务队列</strong>中取出一个事件并把对应的回到加入当前执行栈；如果存在，则会依次执行队列中事件对应的回调，直到<strong>微任务队列</strong>为空，然后去<strong>宏任务队列</strong>中取出最前面的一个事件，把对应的回调加入当前执行栈...如此反复，进入循环。

我们只需记住当当前执行栈执行完毕时会立刻先处理所有<strong>微任务队列</strong>中的事件，然后再去<strong>宏任务队列</strong>中取出一个事件。`同一次事件循环中，微任务永远在宏任务之前执行`

#### 例子
```js
console.log('script start')

async function async1() {
  // async微任务产生的时机:
  // 执行完await之后，
  // 直接跳出async函数，
  // 执行其他代码(此处就是协程的运作，A暂停执行，控制权交给B)。
  // 其他代码执行完毕后，
  // 再回到async函数去执行剩下的代码，
  // 然后把await后面的代码注册到微任务队列当中
  await async2()
  console.log('async1 end')
}

async function async2() {
  console.log('async2 end')
}
async1()

setTimeout(function () {
  console.log('setTimeout')
}, 0)

new Promise((resolve) => {
  console.log('Promise')
  resolve()
})
  .then(function () {
    console.log('promise1')
  })
  .then(function () {
    console.log('promise2')
  })

console.log('script end')
// 旧版Chrome输出:
// script start => 
// async2 end => 
// Promise => 
// script end => 
// promise1 => 
// promise2 => 
// async1 end => 
// setTimeout
```

注意: 新版的chrome浏览器中不是如上打印的，因为chrome优化了,await变得更快了,但是这种做法其实是违法了规范的, 其输出为:
```js
// script start => async2 end => Promise => script end => async1 end => promise1 => promise2 => setTimeout
```

## node环境下的事件循环机制

## 参考链接
[详解JavaScript中的Event Loop(事件循环)机制](https://zhuanlan.zhihu.com/p/33058983)
[一次弄懂Event Loop(彻底解决此类面试问题)](https://juejin.im/post/5c3d8956e51d4511dc72c200#heading-7)
[面试题: 说说事件循环机制(满分答案来了)](https://bit.ly/3bYd5U3)