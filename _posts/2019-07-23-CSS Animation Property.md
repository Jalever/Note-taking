---
layout: post
title: CSS animation Property
subtitle: CSS Properties
date: 2019-07-23
author: Jalever
header-img: img/css_bg_simple.png
catalog: true
tags:
  - CSS
---

- [Introduction](#introduction)
- [Definition and Usage](#definition-and-usage)
- [Browser Support](#browser-support)
- [CSS Syntax](#css-syntax)
- [Property Values](#property-values)
    - [animation-name](#animation-name)
    - [animation-duration](#animation-duration)
    - [animation-timing-function](#animation-timing-function)
    - [animation-delay](#animation-delay)
    - [animation-iteration-count](#animation-iteration-count)
    - [animation-direction](#animation-direction)
    - [animation-fill-mode](#animation-fill-mode)
    - [animation-play-state](#animation-play-state)

## Introduction

HTML Codes
![eknoNR.png](https://s2.ax1x.com/2019/07/23/eknoNR.png)
CSS Codes
![eknT41.png](https://s2.ax1x.com/2019/07/23/eknT41.png)
Result
![eknvHH.png](https://s2.ax1x.com/2019/07/23/eknvHH.png)
![ekuSUA.gif](https://s2.ax1x.com/2019/07/23/ekuSUA.gif)
![ekup4I.png](https://s2.ax1x.com/2019/07/23/ekup4I.png)

## Definition and Usage
The <strong>animation</strong> property is a shorthand property for:
- animation-name
- animation-duration
- animation-timing-function
- animation-delay
- animation-iteration-count
- animation-direction
- animation-fill-mode
- animation-play-state
> Note: Always specify the `animation-duration` property, otherwise the duration is 0, and will never be played.

![eknwng.png](https://s2.ax1x.com/2019/07/23/eknwng.png)

## Browser Support
The numbers in the table specify the first browser version that fully supports the property.

Numbers followed by `-webkit-`, `-moz-`, or `-o-` specify the first version that worked with a prefix.
![ekuEDg.png](https://s2.ax1x.com/2019/07/23/ekuEDg.png)

## CSS Syntax
![ekumUs.png](https://s2.ax1x.com/2019/07/23/ekumUs.png)

## animation-name
<table>
    <thead>
        <tr>
            <td>Value</td>
            <td>Description</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>animation-name</td>
            <td>Specifies the name of the keyframe you want to bind to the selector</td>
        </tr>
        <tr>
            <td>animation-duration</td>
            <td>Specifies how many seconds or milliseconds an animation takes to complete</td>
        </tr>
        <tr>
            <td>animation-timing-function</td>
            <td>Specifies the speed curve of the animation</td>
        </tr>
        <tr>
            <td>animation-delay</td>
            <td>Specifies a delay before the animation will start</td>
        </tr>
        <tr>
            <td>animation-iteration-count</td>
            <td>Specifies how many times an animation should be played</td>
        </tr>
        <tr>
            <td>animation-direction</td>
            <td>Specifies whether or not the animation should play in reverse on alternate cycles</td>
        </tr>
        <tr>
            <td>animation-fill-mode</td>
            <td>Specifies what values are applied by the animation outside the time it is executing</td>
        </tr>
        <tr>
            <td>animation-play-state</td>
            <td>Specifies whether the animation is running or paused</td>
        </tr>
        <tr>
            <td>initial</td>
            <td>Sets this property to its default value.</td>
        </tr>
        <tr>
            <td>inherit</td>
            <td>Inherits this property from its parent element.</td>
        </tr>
    </tbody>
</table>

#### animation-name
#### animation-duration
Specifies the length of time an animation should take to complete one cycle. This can be specified in seconds or milliseconds. Default value is 0, which means that no animation will occur

#### animation-timing-function
The `animation-timing-function` specifies the speed curve of an animation.

The speed curve defines the TIME an animation uses to change from one set of CSS styles to another.

The speed curve is used to make the changes smoothly.
![ek8uef.png](https://s2.ax1x.com/2019/07/23/ek8uef.png)

###### CSS Syntax
![ek83Wj.png](https://s2.ax1x.com/2019/07/23/ek83Wj.png)
The animation-timing-function uses a mathematical function, called the `Cubic Bezier curve`, to make the speed curve. You can use your own values in this function, or use one of the pre-defined values:

###### Property Values
<table>
    <thead>
        <tr>
            <td>Value</td>
            <td>Description</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>linear</td>
            <td>The animation has the same speed from start to end</td>
        </tr>
        <tr>
            <td>ease</td>
            <td>Default value. The animation has a slow start, then fast, before it ends slowly</td>
        </tr>
        <tr>
            <td>ease-in</td>
            <td>The animation has a slow start</td>
        </tr>
        <tr>
            <td>ease-out</td>
            <td>The animation has a slow end</td>
        </tr>
        <tr>
            <td>ease-in-out</td>
            <td>The animation has both a slow start and a slow end</td>
        </tr>
        <tr>
            <td>step-start</td>
            <td>Equivalent to steps(1, start)</td>
        </tr>
        <tr>
            <td>step-end</td>
            <td>Equivalent to steps(1, end)</td>
        </tr>
        <tr>
            <td>steps(int,start|end)</td>
            <td>Specifies a stepping function, with two parameters. The first parameter specifies the number of intervals in the function. It must be a positive integer (greater than 0). The second parameter, which is optional, is either the value "start" or "end", and specifies the point at which the change of values occur within the interval. If the second parameter is omitted, it is given the value "end"</td>
        </tr>
        <tr>
            <td>cubic-bezier(n,n,n,n)</td>
            <td>Define your own values in the cubic-bezier function
Possible values are numeric values from 0 to 1.<br/><br/>The cubic-bezier() function defines a Cubic Bezier curve.<br/><br/>A Cubic Bezier curve is defined by four points P0, P1, P2, and P3. P0 and P3 are the start and the end of the curve and, in CSS these points are fixed as the coordinates are ratios. P0 is (0, 0) and represents the initial time and the initial state, P3 is (1, 1) and represents the final time and the final state.</td>
        </tr>
        <tr>
            <td>initial</td>
            <td>Sets this property to its default value.</td>
        </tr>
        <tr>
            <td>inherit</td>
            <td>Inherits this property from its parent element.</td>
        </tr>
    </tbody>
</table>

#### animation-delay
#### animation-iteration-count
#### animation-direction
#### animation-fill-mode
###### Property Values
<table>
    <thead>
        <tr>
            <td>Value</td>
            <td>Description</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>none</td>
            <td>Default value. Animation will not apply any styles to the element before or after it is executing</td>
        </tr>
        <tr>
            <td>forwards</td>
            <td>The element will retain the style values that is set by the last keyframe (depends on animation-direction and animation-iteration-count)</td>
        </tr>
        <tr>
            <td>backwards</td>
            <td>The element will get the style values that is set by the first keyframe (depends on animation-direction), and retain this during the animation-delay period</td>
        </tr>
        <tr>
            <td>both</td>
            <td>The animation will follow the rules for both forwards and backwards, extending the animation properties in both directions</td>
        </tr>
        <tr>
            <td>initial</td>
            <td>Sets this property to its default value.</td>
        </tr>
        <tr>
            <td>inherit</td>
            <td>Inherits this property from its parent element.</td>
        </tr>
    </tbody>
</table>

<strong>animation-fill-mode: forwards;</strong><br/>
CSS Codes
![ekUO7q.png](https://s2.ax1x.com/2019/07/23/ekUO7q.png)
Result
![ekUqns.gif](https://s2.ax1x.com/2019/07/23/ekUqns.gif)
<br/>
<strong>animation-fill-mode: backwards;</strong><br/>
CSS Codes
![ekUhAP.png](https://s2.ax1x.com/2019/07/23/ekUhAP.png)
Result
![ekU5h8.gif](https://s2.ax1x.com/2019/07/23/ekU5h8.gif)

#### animation-play-state
