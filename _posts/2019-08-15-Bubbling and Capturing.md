---
layout: post
title: Bubbling and capturing
subtitle: Introduction to Events
date: 2019-08-15
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - JavaScript
---

Let’s start with an example.

This handler is assigned to &lt;div&gt;, but also runs if you click any nested tag like &lt;em&gt; or &lt;code&gt;:
![mAd7tS.png](https://s2.ax1x.com/2019/08/15/mAd7tS.png)

## Bubbling
The bubbling principle is simple.

<strong>When an event happens on an element, it first runs the handlers on it, then on its parent, then all the way up on other ancestors</strong>.

Let’s say we have 3 nested elements `FORM > DIV > P` with a handler on each of them:
![mA0QaV.png](https://s2.ax1x.com/2019/08/15/mA0QaV.png)
![mA0NrR.png](https://s2.ax1x.com/2019/08/15/mA0NrR.png)

A click on the inner <p> first runs onclick:

1. On that &lt;p&gt;.
2. Then on the outer &lt;div&gt;.
3. Then on the outer &lt;form&gt;.
4. And so on upwards till the document object.

![mA0cMd.png](https://s2.ax1x.com/2019/08/15/mA0cMd.png)
So if we click on <strong>&lt;p&gt;</strong>, then we’ll see 3 alerts: `p -> div -> form`.

The process is called “bubbling”, because events “bubble” from the inner element up through parents like a bubble in the water.

> <strong>Almost all events bubble</strong>.<br/>
> The key word in this phrase is “almost”.<br/>
> For instance, a focus event does not bubble. There are other examples too, we’ll meet them. But still it’s an exception, rather than a rule, most events do bubble.

## event.target
A handler on a parent element can always get the details about where it actually happened.

The most deeply nested element that caused the event is called a target element, accessible as `event.target`.

Note the differences from `this` (=`event.currentTarget`):

- `event.target` – is the “target” element that initiated the event, it doesn’t change through the bubbling process.
- `this` – is the “current” element, the one that has a currently running handler on it.

For instance, if we have a single handler `form.onclick`, then it can “catch” all clicks inside the form. No matter where the click happened, it bubbles up to <strong>&lt;form&gt;</strong> and runs the handler.

In `form.onclick` handler:

- `this` (=`event.currentTarget`) is the <strong>&lt;form&gt;</strong> element, because the handler runs on it.
- `event.target` is the actual element inside the form that was clicked.

Check it out:
<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="css,result" data-user="Jalever" data-slug-hash="YzKqNWV" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Bubbling and Capturing">
  <span>See the Pen <a href="https://codepen.io/Jalever/pen/YzKqNWV/">
  Bubbling and Capturing</a> by Jalever Chen (<a href="https://codepen.io/Jalever">@Jalever</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

It’s possible that <strong>event.target</strong> could equal <strong>this</strong> – it happens when the click is made directly on the <strong>&lt;form&gt;</strong> element.

## Stopping bubbling



## Capturing





## Summary
