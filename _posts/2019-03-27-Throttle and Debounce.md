---
layout: post
title: Throttle and Debounce
subtitle: Web Development
date: 2019-03-27
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Web Development
---

Event trigger rate is the number of times an event handler invokes in a given amount of time.<br/>
In general, mouse clicks have lower event trigger rates compare to scrolling and mouseover.

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



## Debounce
debouncing is a technique to prevent the event trigger from being fired too often.<br/>

<ins>***Debouncing***</ins> enforces that a function not be called again until a certain amount of time has passed without it being called.<br>

As in "execute this function only if 100 milliseconds have passed without it being called."
Perhaps a function is called 1,000 times in a quick burst, dispersed over 3 seconds, then stops being called. <br>

If you have debounced it at 100 milliseconds, the function will only fire once, at 3.1 seconds, once the burst is over. <br>

Each time the function is called during the burst it resets the debouncing timer.
