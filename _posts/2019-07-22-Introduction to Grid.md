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
- [Introduction](#introduction)
- [Important Terminology](#important-terminology)
    - [Grid Container](#grid-container)
    - [Grid Item](#grid-item)
    - [Grid Line](#grid-line)
    - [Grid Track](#grid-track)
    - [Grid Cell](#grid-cell)
    - [Grid Area](#grid-area)
- [Grid Properties Table of Contents](#grid-properties-table-of-contents)
    - [Properties for the Grid Container](#properties-for-the-grid-container)
        - [display](#display)
        - [grid-template-columns](#grid-template-columns)
        - [grid-template-rows](#grid-template-rows)
        - [grid-template-areas](#grid-template-areas)

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

## Grid Properties Table of Contents
#### Properties for the Grid Container
###### display
Defines the element as a grid container and establishes a new grid formatting context for its contents.

Values:
- <strong>grid</strong> - generates a block-level grid
- <strong>inline-grid</strong> - generates an inline-level grid

![eCqio6.png](https://s2.ax1x.com/2019/07/22/eCqio6.png)

###### grid-template-columns
###### grid-template-rows
Defines the columns and rows of the grid with a space-separated list of values. The values represent the track size, and the space between them represents the grid line.

Values:
- <strong>&#60;track-size&#62;</strong> - can be a length, a percentage, or a fraction of the free space in the grid (using the fr unit)
- <strong>&#60;line-name&#62;</strong> - an arbitrary name of your choosing
![eCjVAI.png](https://s2.ax1x.com/2019/07/22/eCjVAI.png)

Examples:

When you leave an empty space between the track values, the grid lines are automatically assigned positive and negative numbers:
![eCj1Bj.png](https://s2.ax1x.com/2019/07/22/eCj1Bj.png)
![eCjU3T.png](https://s2.ax1x.com/2019/07/22/eCjU3T.png)

But you can choose to explicitly name the lines. Note the bracket syntax for the line names:
![eCj28K.png](https://s2.ax1x.com/2019/07/22/eCj28K.png)
![eCjRgO.png](https://s2.ax1x.com/2019/07/22/eCjRgO.png)

Note that a line can have more than one name. For example, here the second line will have two names: row1-end and row2-start:
![eCjWvD.png](https://s2.ax1x.com/2019/07/22/eCjWvD.png)

If your definition contains repeating parts, you can use the `repeat()` notation to streamline things:
![eCvF2T.png](https://s2.ax1x.com/2019/07/22/eCvF2T.png)
Which is equivalent to this:
![eCvMPx.png](https://s2.ax1x.com/2019/07/22/eCvMPx.png)

If multiple lines share the same name, they can be referenced by their line name and count.
![eCvGse.png](https://s2.ax1x.com/2019/07/22/eCvGse.png)

The `fr` unit allows you to set the size of a track as a fraction of the free space of the grid container. For example, this will set each item to one third the width of the grid container:
![eCvBz8.png](https://s2.ax1x.com/2019/07/22/eCvBz8.png)

The free space is calculated after any non-flexible items. In this example the total amount of free space available to the `fr` units doesn't include the 50px:
![eCvcZj.png](https://s2.ax1x.com/2019/07/22/eCvcZj.png)

###### grid-template-areas
Defines a grid template by referencing the names of the grid areas which are specified with the `grid-area` property. Repeating the name of a grid area causes the content to span those cells. A period signifies an empty cell. The syntax itself provides a visualization of the structure of the grid.

Values:<br/>
- <strong>&#60;grid-area-name&#62;</strong> - the name of a grid area specified with grid-area
- <strong>.</strong> - a period signifies an empty grid cell
- <strong>none</strong> - no grid areas are defined
![ePwWrR.png](https://s2.ax1x.com/2019/07/22/ePwWrR.png)

Example:
![eP0ALn.png](https://s2.ax1x.com/2019/07/22/eP0ALn.png)

That'll create a grid that's four columns wide by three rows tall. The entire top row will be comprised of the <strong>header</strong> area. The middle row will be comprised of two <strong>main</strong> areas, one empty cell, and one <strong>sidebar</strong> area. The last row is all <strong>footer</strong>.
![eP0Mz4.png](https://s2.ax1x.com/2019/07/22/eP0Mz4.png)

Each row in your declaration needs to have the same number of cells.

You can use any number of adjacent periods to declare a single empty cell. As long as the periods have no spaces between them they represent a single cell.

Notice that you're not naming lines with this syntax, just areas. When you use this syntax the lines on either end of the areas are actually getting named automatically. If the name of your grid area is <strong>foo</strong>, the name of the area's starting row line and starting column line will be <strong>foo-start</strong>, and the name of its last row line and last column line will be <strong>foo-end</strong>. This means that some lines might have multiple names, such as the far left line in the above example, which will have three names: header-start, main-start, and footer-start.
