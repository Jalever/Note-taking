---
layout: post
title: Throttle and Debounce
subtitle: Web Development学习笔记系列
date: 2019-03-26
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - JavaScript
  - Web Development
---

## Throttle[节流]
<ins>***Throttling***</ins> enforces a maximum number of times a function can be called over time. <br>
As in "execute this function at most once every 100 milliseconds."

Say under normal circumstances you would call this function 1,000 times over 10 seconds. 
<br>If you throttle it to only once per 100 milliseconds, it would only execute that function at most 100 times<br>
(10s * 1,000) = 10,000ms<br>
(10,000ms / 100ms) throttling = 100 maximum calls
&nbsp;&nbsp;节流，是指频繁触发事件时，只会在指定的时间段内执行事件回调，即触发事件间隔大于等于指定的时间才会执行回调函数


## Debounce[防抖]
<ins>***Debouncing***</ins> enforces that a function not be called again until a certain amount of time has passed without it being called.<br> 
As in "execute this function only if 100 milliseconds have passed without it being called."
Perhaps a function is called 1,000 times in a quick burst, dispersed over 3 seconds, then stops being called. <br> 
If you have debounced it at 100 milliseconds, the function will only fire once, at 3.1 seconds, once the burst is over. <br> 
Each time the function is called during the burst it resets the debouncing timer.
&nbsp;&nbsp;就是指触发事件后，就是把触发非常频繁的事件合并成一次去执行<br>
&nbsp;&nbsp;在指定时间内只执行一次回调函数，如果在指定的时间内又触发了该事件，则回调函数的执行时间会基于此刻重新开始计算<br>
&nbsp;&nbsp;以我们生活中乘车刷卡的情景举例，只要乘客不断地在刷卡，司机师傅就不能开车，乘客刷卡完毕之后，司机会等待几分钟，确定乘客坐稳再开车。如果司机在最后等待的时间内又有新的乘客上车，那么司机等乘客刷卡完毕之后，还要再等待一会，等待所有乘客坐稳再开车<br>

## 两者之间的区别
频繁触发事件时，`函数防抖`只会在最后一次触发事件只会才会执行回调内容，其他情况下会重新计算延迟事件，而`函数节流`便会很有规律的每隔一定时间执行一次回调函数
