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
- [Throttle](#throttle)

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

## Throttle
In a nutshell, throttling means delaying function execution.<br/>

So instead of executing the event handler/function immediately, you’ll be adding a few milliseconds of delay when an event is triggered.<br/>

This can be used when implementing infinite scrolling, for example. <br/>

Rather than fetching the next result set as the user is scrolling, you can delay the XHR call.<br/>

Another good example of this is Ajax-based instant search. <br/>

You might not want to hit the server for every key press, so it’s better to throttle until the input field is dormant for a few milliseconds.<br/>

<ins>***Throttling***</ins> enforces a maximum number of times a function can be called over time. <br>

As in "execute this function at most once every 100 milliseconds."

Say under normal circumstances you would call this function 1,000 times over 10 seconds.
<br>

If you throttle it to only once per 100 milliseconds, it would only execute that function at most 100 times<br>

(10s * 1,000) = 10,000ms<br>

(10,000ms / 100ms) throttling = 100 maximum calls



