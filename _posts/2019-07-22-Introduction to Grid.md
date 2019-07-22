---
layout: post
title: Introduction to Grid
subtitle: A Complete Guide to Grid
date: 2019-07-22
author: Jalever
header-img: img/css_bg_simple.png
catalog: true
tags:
  - CSS
---

## Introduction
<strong>CSS Grid Layout</strong> is the most powerful layout system available in <strong>CSS</strong>. It is a 2-dimensional system, meaning it can handle both columns and rows, unlike <strong>Flexbox</strong> which is largely a 1-dimensional system. You work with <strong>Grid Layout</strong> by applying <strong>CSS</strong> rules both to a parent element (which becomes the <strong>Grid Container</strong>) and to that element's children (which become <strong>Grid Items</strong>).

<strong>CSS Grid Layout</strong> (aka "Grid"), is a two-dimensional grid-based layout system that aims to do nothing less than completely change the way we design grid-based user interfaces. <strong>CSS</strong> has always been used to lay out our web pages, but it's never done a very good job of it. First, we used <ins>table</ins>s, then <ins>float</ins>s, <ins>positioning</ins> and <ins>inline-block</ins>, but all of these methods were essentially hacks and left out a lot of important functionality (vertical centering, for instance). <strong>Flexbox</strong> helped out, but it's intended for simpler one-dimensional layouts, not complex two-dimensional ones (<strong>Flexbox</strong> and <strong>Grid</strong> actually work very well together). <strong>Grid</strong> is the very first <strong>CSS</strong> module created specifically to solve the layout problems we've all been hacking our way around for as long as we've been making websites.

## Important Terminology
#### Grid Container
The element on which `display: grid` is applied. It's the direct parent of all the grid items. In this example `container` is the grid container.
![eCHMjA.png](https://s2.ax1x.com/2019/07/22/eCHMjA.png)

#### Grid Item
The children (i.e. direct descendants) of the grid container. Here the `item` elements are grid items, but `sub-item` isn't.
![eCHWv9.png](https://s2.ax1x.com/2019/07/22/eCHWv9.png)

#### Grid Line
The dividing lines that make up the structure of the grid. They can be either vertical ("column grid lines") or horizontal ("row grid lines") and reside on either side of a row or column. Here the yellow line is an example of a column grid line.
![eCHbCD.png](https://s2.ax1x.com/2019/07/22/eCHbCD.png)

#### Grid Track
The space between two adjacent grid lines. You can think of them like the columns or rows of the grid. Here's the grid track between the second and third row grid lines.
![eCHjKA.png](https://s2.ax1x.com/2019/07/22/eCHjKA.png)

#### Grid Cell
The space between two adjacent row and two adjacent column grid lines. It's a single "unit" of the grid. Here's the grid cell between row grid lines 1 and 2, and column grid lines 2 and 3.
![eCb958.png](https://s2.ax1x.com/2019/07/22/eCb958.png)

#### Grid Area
The total space surrounded by four grid lines. A grid area may be comprised of any number of grid cells. Here's the grid area between row grid lines 1 and 3, and column grid lines 1 and 3.
![eCbi8g.png](https://s2.ax1x.com/2019/07/22/eCbi8g.png)
