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
A bubbling event goes from the target element straight up. Normally it goes upwards till <strong>&lt;html&gt;</strong>, and then to <strong>document</strong> object, and some events even reach <strong>window</strong>, calling all handlers on the path.

But any handler may decide that the event has been fully processed and stop the bubbling.

The method for it is <strong>event.stopPropagation()</strong>.

For instance, here <strong>body.onclick</strong> doesn’t work if you click on <strong>&lt;button&gt;</strong>:

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="html,result" data-user="Jalever" data-slug-hash="oNvxBBB" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="stopBubbling">
  <span>See the Pen <a href="https://codepen.io/Jalever/pen/oNvxBBB/">
  stopBubbling</a> by Jalever Chen (<a href="https://codepen.io/Jalever">@Jalever</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

> <strong>event.stopImmediatePropagation()</strong><br/><br/>
> If an element has multiple event handlers on a single event, then even if one of them stops the bubbling, the other ones still execute.<br/><br/>
> In other words, `event.stopPropagation()` stops the move upwards, but on the current element all other handlers will run.<br/><br/>
> To stop the bubbling and prevent handlers on the current element from running, there’s a method `event.stopImmediatePropagation()`. After it no other handlers execute.

> Don’t stop bubbling without a need!<br/>
> Bubbling is convenient. Don’t stop it without a real need: obvious and architecturally well-thought.<br/>
> Sometimes `event.stopPropagation()` creates hidden pitfalls that later may become problems.<br/><br/>
> For instance:<br/>
> We create a nested menu. Each submenu handles clicks on its elements and calls `stopPropagation` so that the outer menu won’t trigger.<br/>
> Later we decide to catch clicks on the whole window, to track users’ behavior (where people click). Some analytic systems do that. Usually the code uses `document.addEventListener('click'…)` to catch all clicks.<br/>
> Our analytic won’t work over the area where clicks are stopped by `stopPropagation`. Sadly, we’ve got a “dead zone”.<br/><br/>
> There’s usually no real need to prevent the bubbling. A task that seemingly requires that may be solved by other means. One of them is to use custom events, we’ll cover them later. Also we can write our data into the `event` object in one handler and read it in another one, so we can pass to handlers on parents information about the processing below.

## Capturing
There’s another phase of event processing called “capturing”. It is rarely used in real code, but sometimes can be useful.

The standard DOM Events describes 3 phases of event propagation:

1. <strong>Capturing phase</strong> – the event goes down to the element.
2. <strong>Target phase</strong> – the event reached the target element.
3. <strong>Bubbling phase</strong> – the event bubbles up from the element.

Here’s the picture of a click on &lt;td&gt; inside a table, taken from the specification:
![mA6PVs.png](https://s2.ax1x.com/2019/08/15/mA6PVs.png)

That is: for a click on <strong>&lt;td&gt;</strong> the event first goes through the ancestors chain down to the element (capturing phase), then it reaches the target and triggers there (target phase), and then it goes up (bubbling phase), calling handlers on its way.

<strong>Before we only talked about bubbling, because the capturing phase is rarely used. Normally it is invisible to us.</strong>

Handlers added using <strong>on&lt;event&gt;</strong>-property or using HTML attributes or using two-argument <strong>addEventListener(event, handler)</strong> don’t know anything about capturing, they only run on the 2nd and 3rd phases.

To catch an event on the capturing phase, we need to set the handler <strong>capture</strong> option to <strong>true</strong>:
![mA6Dit.png](https://s2.ax1x.com/2019/08/15/mA6Dit.png)
There are two possible values of the <strong>capture</strong> option:

- If it’s <strong>false</strong> (default), then the handler is set on the bubbling phase.
- If it’s <strong>true</strong>, then the handler is set on the capturing phase.
Note that while formally there are 3 phases, the 2nd phase (“target phase”: the event reached the element) is not handled separately: handlers on both capturing and bubbling phases trigger at that phase.

Let’s see both capturing and bubbling in action:
<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="html,result" data-user="Jalever" data-slug-hash="NWKNdvE" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Capturing">
  <span>See the Pen <a href="https://codepen.io/Jalever/pen/NWKNdvE/">
  Capturing</a> by Jalever Chen (<a href="https://codepen.io/Jalever">@Jalever</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

The code sets click handlers on every element in the document to see which ones are working.

If you click on <strong>&lt;p&gt;</strong>, then the sequence is:

1. `HTML` → `BODY` → `FORM` → `DIV` (capturing phase, the first listener):
2. `P` (target phrase, triggers two times, as we’ve set two listeners: capturing and bubbling)
3. `DIV` → `FORM` → `BODY` → `HTML` (bubbling phase, the second listener).

There’s a property `event.eventPhase` that tells us the number of the phase on which the event was caught. But it’s rarely used, because we usually know it in the handler.

> <strong>To remove the handler, removeEventListener needs the same phase</strong><br/>
> If we `addEventListener(..., true)`, then we should mention the same phase in `removeEventListener(..., true)` to correctly remove the handler.

> <strong>Listeners on same element and same phase run in their set order</strong><br/>
> If we have multiple event handlers on the same phase, assigned to the same element with `addEventListener`, they run in the same order as they are created:

## Summary
When an event happens – the most nested element where it happens gets labeled as the “target element” (`event.target`).

- Then the event moves down from the document root to `event.target`, calling handlers assigned with `addEventListener(...., true)` on the way (`true` is a shorthand for `{capture: true}`).
- Then handlers are called on the target element itself.
- Then the event bubbles up from `event.target` up to the root, calling handlers assigned using <strong>on&lt;event&gt;</strong> and `addEventListener` without the 3rd argument or with the 3rd argument `false`/`{capture:false}`.

Each handler can access `event` object properties:

- <strong>event.target</strong> – the deepest element that originated the event.
- <strong>event.currentTarget</strong> (=<strong>this</strong>) – the current element that handles the event (the one that has the handler on it)
- <strong>event.eventPhase</strong> – the current phase (capturing=1, target=2, bubbling=3).

Any event handler can stop the event by calling `event.stopPropagation()`, but that’s not recommended, because we can’t really be sure we won’t need it above, maybe for completely different things.

The capturing phase is used very rarely, usually we handle events on bubbling. And there’s a logic behind that.

In real world, when an accident happens, local authorities react first. They know best the area where it happened. Then higher-level authorities if needed.

The same for event handlers. The code that set the handler on a particular element knows maximum details about the element and what it does. A handler on a particular &lt;td&gt; may be suited for that exactly &lt;td&gt;, it knows everything about it, so it should get the chance first. Then its immediate parent also knows about the context, but a little bit less, and so on till the very top element that handles general concepts and runs the last.

Bubbling and capturing lay the foundation for “event delegation” – an extremely powerful event handling pattern that we study in the next chapter.
