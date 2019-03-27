---
layout: post
title: Throttle and Debounce
subtitle: Web Development
date: 2019-03-26
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - JavaScript
---

## Throttle[防抖]
&ensp;&ensp;<ins>***Throttling***</ins> enforces a maximum number of times a function can be called over time. As in "execute this function at most once every 100 milliseconds."

&ensp;&ensp;Say under normal circumstances you would call this function 1,000 times over 10 seconds. If you throttle it to only once per 100 milliseconds, it would only execute that function at most 100 times

(10s * 1,000) = 10,000ms
10,000ms / 100ms throttling = 100 maximum calls

## Debounce[节流]
&ensp;&ensp;<ins>***Debouncing***</ins> enforces that a function not be called again until a certain amount of time has passed without it being called. As in "execute this function only if 100 milliseconds have passed without it being called."

&ensp;&ensp;Perhaps a function is called 1,000 times in a quick burst, dispersed over 3 seconds, then stops being called. If you have debounced it at 100 milliseconds, the function will only fire once, at 3.1 seconds, once the burst is over. Each time the function is called during the burst it resets the debouncing timer.