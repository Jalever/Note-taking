---
layout: post
title: 防抖Debounce和节流Throttle的原理和实现
subtitle: JavaScript原理和实现系列
date: 2019-03-27
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - JavaScript
---

- [防抖Debounce](#%e9%98%b2%e6%8a%96debounce)
    - [防抖Debounce实现](#%e9%98%b2%e6%8a%96debounce%e5%ae%9e%e7%8e%b0)
- [节流Throttle](#%e8%8a%82%e6%b5%81throttle)

## 防抖Debounce

如果事件在即将计时快结束时又被触发了，那么重新计时

#### 防抖Debounce实现
![GiiO1g.png](https://s1.ax1x.com/2020/03/27/GiiO1g.png)
```js
debounce(fun, delay) {
  return function(args){
    let _args = args;
    let that = this;

    clearTimeout(fun.id);

    fun.id = setTimeout(() => {
      fun.call(that, _args);
    }, delay)
  }
}
```

## 节流Throttle
`throttle`就是设置固定的函数执行速率, 从而降低频繁事件回调的执行次数

![GY3O3V.png](https://s1.ax1x.com/2020/04/02/GY3O3V.png)

变量进行存储:
```js
prevTime: null,
deferTimer: null,
```

实现函数:
```js
handleOutput(e) {
  console.log(e);
},
throttleFn(e) {
  this.throttle(this.handleOutput, 1000)(e.target.value);
},
throttle(func, delay) {
  let that = this;
  return function() {
    let _args = arguments;
    let curTime = +new Date();

    if (that.prevTime && curTime < that.prevTime + delay) {
      clearTimeout(that.deferTimer);
      that.deferTimer = setTimeout(() => {
        that.prevTime = curTime;
        func.apply(that, _args);
      }, delay);
    } else {
      that.prevTime = curTime;
      func.apply(that, _args);
    }
  };
},
```

调用例子:
```js
<el-input v-model="form.username" @keyup.native="throttleFn"></el-input>
```


