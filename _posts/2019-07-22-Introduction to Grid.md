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
    - [Properties for the Grid Container(Grid Container)](#properties-for-the-grid-containergrid-container)
        - [display](#display)
        - [grid-template-columns](#grid-template-columns)
        - [grid-template-rows](#grid-template-rows)
        - [grid-template-areas](#grid-template-areas)
        - [grid-template](#grid-template)
        - [grid-column-gap](#grid-column-gap)
        - [grid-row-gap](#grid-row-gap)
        - [grid-gap](#grid-gap)
        - [justify-items](#justify-items)
        - [align-items](#align-items)
        - [place-items](#place-items)
        - [justify-content](#justify-content)
        - [align-content](#align-content)
        - [place-content](#place-content)
        - [grid-auto-columns](#grid-auto-columns)
        - [grid-auto-rows](#grid-auto-rows)
        - [grid-auto-flow](#grid-auto-flow)
        - [grid](#grid)
    - [Properties for the Children(Grid Items)](#properties-for-the-childrengrid-items)
        - [grid-column-start](#grid-column-start)
        - [grid-column-end](#grid-column-end)
        - [grid-row-start](#grid-row-start)
        - [grid-row-end](#grid-row-end)
        - [grid-column](#grid-column)
        - [grid-row](#grid-row)
        - [grid-area](#grid-area)
        - [justify-self](#justify-self)
        - [align-self](#align-self)
        - [place-self](#place-self)
        
## Introduction
<strong>CSS Grid Layout</strong> is the most powerful layout system available in <strong>CSS</strong>. It is a 2-dimensional system, meaning it can handle both columns and rows, unlike <strong>Flexbox</strong> which is largely a 1-dimensional system. You work with <strong>Grid Layout</strong> by applying <strong>CSS</strong> rules both to a parent element (which becomes the <strong>Grid Container</strong>) and to that element's children (which become <strong>Grid Items</strong>).

<strong>CSS Grid Layout</strong> (aka "Grid"), is a two-dimensional grid-based layout system that aims to do nothing less than completely change the way we design grid-based user interfaces. <strong>CSS</strong> has always been used to lay out our web pages, but it's never done a very good job of it. First, we used <ins>table</ins>s, then <ins>float</ins>s, <ins>positioning</ins> and <ins>inline-block</ins>, but all of these methods were essentially hacks and left out a lot of important functionality (vertical centering, for instance). <strong>Flexbox</strong> helped out, but it's intended for simpler one-dimensional layouts, not complex two-dimensional ones (<strong>Flexbox</strong> and <strong>Grid</strong> actually work very well together). <strong>Grid</strong> is the very first <strong>CSS</strong> module created specifically to solve the layout problems we've all been hacking our way around for as long as we've been making websites.
![ePOk6g.png](https://s2.ax1x.com/2019/07/22/ePOk6g.png)
![ePOZ0s.png](https://s2.ax1x.com/2019/07/22/ePOZ0s.png)

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
#### Properties for the Grid Container(Grid Container)
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

###### grid-template
A shorthand for setting <strong>grid-template-rows</strong>, <strong>grid-template-columns</strong>, and <strong>grid-template-areas</strong> in a single declaration.

Values:<br/>
- <strong>none</strong> - sets all three properties to their initial values
- <strong>&#60;grid-template-rows&#62;</strong> / <strong>&#60;grid-template-columns&#62;</strong> - sets - `grid-template-columns` and - - `grid-template-rows` to the specified values, respectively, and sets `grid-template-areas` to `none`
![ePRPAJ.png](https://s2.ax1x.com/2019/07/22/ePRPAJ.png)

It also accepts a more complex but quite handy syntax for specifying all three. Here's an example:
![ePRGgP.png](https://s2.ax1x.com/2019/07/22/ePRGgP.png)
That's equivalent to this:
![ePR5CR.png](https://s2.ax1x.com/2019/07/22/ePR5CR.png)
Since `grid-template` doesn't reset the implicit grid properties (`grid-auto-columns`, `grid-auto-rows`, and `grid-auto-flow`), which is probably what you want to do in most cases, it's recommended to use the `grid` property instead of `grid-template`.

###### grid-column-gap
###### grid-row-gap
Specifies the size of the grid lines. You can think of it like setting the width of the gutters between the columns/rows.

Values:<br/>
- &#60;line-size&#62; - a length value
![ePfUYj.png](https://s2.ax1x.com/2019/07/22/ePfUYj.png)
Example:
![ePfB60.png](https://s2.ax1x.com/2019/07/22/ePfB60.png)
![ePf2tJ.png](https://s2.ax1x.com/2019/07/22/ePf2tJ.png)
The gutters are only created between the columns/rows, not on the outer edges.

> Note: The `grid-` prefix will be removed and `grid-column-gap` and `grid-row-gap` renamed to `column-gap` and `row-gap`. The unprefixed properties are already supported in Chrome 68+, Safari 11.2 Release 50+ and Opera 54+.

###### grid-gap
A shorthand for `grid-row-gap` and `grid-column-gap`

Values:<br/>
- <strong>&#60;grid-row-gap&#62;</strong> <strong>&#60;grid-column-gap&#62;</strong> - length values
![ePhUHO.png](https://s2.ax1x.com/2019/07/22/ePhUHO.png)
Example:
![ePhwUe.png](https://s2.ax1x.com/2019/07/22/ePhwUe.png)

If no `grid-row-gap` is specified, it's set to the same value as `grid-column-gap`

> Note: The `grid-` prefix will be removed and `grid-gap` renamed to `gap`. The unprefixed property is already supported in Chrome 68+, Safari 11.2 Release 50+ and Opera 54+.

###### justify-items
Aligns grid items along the <ins>inline (row) axis</ins> (as opposed to `align-items` which aligns along the <ins>block (column) axis</ins>). This value applies to all grid items inside the container.

Values:<br/>
- <strong>start</strong> - aligns items to be flush with the start edge of their cell
- <strong>end</strong> - aligns items to be flush with the end edge of their cell
- <strong>center</strong> - aligns items in the center of their cell
- <strong>stretch</strong> - fills the whole width of the cell (this is the default)
![ePTJ00.png](https://s2.ax1x.com/2019/07/22/ePTJ00.png)

Examples:
![ePTNkT.png](https://s2.ax1x.com/2019/07/22/ePTNkT.png)
![ePT2tO.png](https://s2.ax1x.com/2019/07/22/ePT2tO.png)
![ePTL4S.png](https://s2.ax1x.com/2019/07/22/ePTL4S.png)
![ePTvcj.png](https://s2.ax1x.com/2019/07/22/ePTvcj.png)
![eP7qq1.png](https://s2.ax1x.com/2019/07/22/eP7qq1.png)
![ePHAdP.png](https://s2.ax1x.com/2019/07/22/ePHAdP.png)
![eP7dVP.png](https://s2.ax1x.com/2019/07/22/eP7dVP.png)
![eP75PU.png](https://s2.ax1x.com/2019/07/22/eP75PU.png)
This behavior can also be set on individual grid items via the `justify-self` property.

###### align-items
Aligns grid items along the <ins>block (column) axis</ins> (as opposed to `justify-items` which aligns along the <ins>inline (row) axis</ins>). This value applies to all grid items inside the container.

Values:
- <strong>start</strong> - aligns items to be flush with the start edge of their cell
- <strong>end</strong> - aligns items to be flush with the end edge of their cell
- <strong>center</strong> - aligns items in the center of their cell
- <strong>stretch</strong> - fills the whole height of the cell (this is the default)
![ePbpkV.png](https://s2.ax1x.com/2019/07/22/ePbpkV.png)
Examples:
![ePbVmR.png](https://s2.ax1x.com/2019/07/22/ePbVmR.png)
![ePbl1e.png](https://s2.ax1x.com/2019/07/22/ePbl1e.png)
![ePbah8.png](https://s2.ax1x.com/2019/07/22/ePbah8.png)
![ePqSud.png](https://s2.ax1x.com/2019/07/22/ePqSud.png)
This behavior can also be set on individual grid items via the `align-self` property.

###### place-items
`place-items` sets both the `align-items` and `justify-items` properties in a single declaration.

Values:<br/>
- <strong>&#60;align-items&#62;</strong> / <strong>&#60;justify-items&#62;</strong> - The first value sets `align-items`, the second value `justify-items`. If the second value is omitted, the first value is assigned to both properties.

All major browsers except Edge support the `place-items` shorthand property.

###### justify-content
Sometimes the total size of your grid might be less than the size of its grid container. This could happen if all of your grid items are sized with non-flexible units like `px`. In this case you can set the alignment of the grid within the grid container. This property aligns the grid along the inline (row) axis (as opposed to `align-content` which aligns the grid along the block (column) axis).

Values:
- <strong>start</strong> - aligns the grid to be flush with the start edge of the grid container
- <strong>end</strong> - aligns the grid to be flush with the end edge of the grid container
- <strong>center</strong> - aligns the grid in the center of the grid container
- <strong>stretch</strong> - resizes the grid items to allow the grid to fill the full width of the grid container
- <strong>space-around</strong> - places an even amount of space between each grid item, with half-sized spaces on the far ends
- <strong>space-between</strong> - places an even amount of space between each grid item, with no space at the far ends
- <strong>space-evenly</strong> - places an even amount of space between each grid item, including the far ends
![ePjLlT.png](https://s2.ax1x.com/2019/07/22/ePjLlT.png)

Examples:
![ePv9t1.png](https://s2.ax1x.com/2019/07/22/ePv9t1.png)
![ePvk6O.png](https://s2.ax1x.com/2019/07/22/ePvk6O.png)
![ePvVne.png](https://s2.ax1x.com/2019/07/22/ePvVne.png)
![ePvnAA.png](https://s2.ax1x.com/2019/07/22/ePvnAA.png)
![ePvQ9P.png](https://s2.ax1x.com/2019/07/22/ePvQ9P.png)
![ePvGng.png](https://s2.ax1x.com/2019/07/22/ePvGng.png)
![ePvqUA.png](https://s2.ax1x.com/2019/07/22/ePvqUA.png)

###### align-content
Sometimes the total size of your grid might be less than the size of its grid container. This could happen if all of your grid items are sized with non-flexible units like `px`. In this case you can set the alignment of the grid within the grid container. This property aligns the grid along the block (column) axis (as opposed to `justify-content` which aligns the grid along the inline (row) axis).

Values:
- <strong>start</strong> - aligns the grid to be flush with the start edge of the grid container
- <strong>end</strong> - aligns the grid to be flush with the end edge of the grid container
- <strong>center</strong> - aligns the grid in the center of the grid container
- <strong>stretch</strong> - resizes the grid items to allow the grid to fill the full height of the grid container
- <strong>space-around</strong> - places an even amount of space between each grid item, with half-sized spaces on the far ends
- <strong>space-between</strong> - places an even amount of space between each grid item, with no space at the far ends
- <strong>space-evenly</strong> - places an even amount of space between each grid item, including the far ends
![ePzAdH.png](https://s2.ax1x.com/2019/07/22/ePzAdH.png)

Examples:
![ePzuSP.png](https://s2.ax1x.com/2019/07/22/ePzuSP.png)
![ePz8oj.png](https://s2.ax1x.com/2019/07/22/ePz8oj.png)
![ePzBmF.png](https://s2.ax1x.com/2019/07/22/ePzBmF.png)
![ePzx0g.png](https://s2.ax1x.com/2019/07/22/ePzx0g.png)
![eiSa4A.png](https://s2.ax1x.com/2019/07/22/eiSa4A.png)
![eiS4g0.png](https://s2.ax1x.com/2019/07/22/eiS4g0.png)
![eiS4g0.png](https://s2.ax1x.com/2019/07/22/eiS4g0.png)

###### place-content
`place-content` sets both the `align-content` and `justify-content` properties in a single declaration.

Values:
- <strong>&#60;align-content&#62;</strong> / <strong>&#60;justify-content&#62;</strong> - The first value sets `align-content`, the second value `justify-content`. If the second value is omitted, the first value is assigned to both properties.

All major browsers except Edge support the `place-content` shorthand property.

###### grid-auto-columns
###### grid-auto-rows
Specifies the size of any auto-generated grid tracks (aka <ins>implicit grid tracks</ins>). Implicit tracks get created when there are more grid items than cells in the grid or when a grid item is placed outside of the explicit grid.

Values:
- <strong>&#60;track-size&#62;</strong> - can be a length, a percentage, or a fraction of the free space in the grid (using the `fr` unit)
![eikAPg.png](https://s2.ax1x.com/2019/07/22/eikAPg.png)
To illustrate how implicit grid tracks get created, think about this:
![eikmMn.png](https://s2.ax1x.com/2019/07/22/eikmMn.png)
This creates a 2 x 2 grid.

But now imagine you use `grid-column` and `grid-row` to position your grid items like this:
![eiksRH.png](https://s2.ax1x.com/2019/07/22/eiksRH.png)
We told `.item-b` to start on column line 5 and end at column line 6, but we never defined a column line 5 or 6. Because we referenced lines that don't exist, implicit tracks with widths of 0 are created to fill in the gaps. We can use `grid-auto-columns` and `grid-auto-rows` to specify the widths of these implicit tracks:
![eikfdf.png](https://s2.ax1x.com/2019/07/22/eikfdf.png)

###### grid-auto-flow
If you have grid items that you don't explicitly place on the grid, the <i>auto-placement</i> algorithm kicks in to automatically place the items. This property controls how the auto-placement algorithm works.

Values:
- <strong>row</strong> - tells the auto-placement algorithm to fill in each row in turn, adding new rows as necessary (default)
- <strong>column</strong> - tells the auto-placement algorithm to fill in each column in turn, adding new columns as necessary
- <strong>dense</strong> - tells the auto-placement algorithm to attempt to fill in holes earlier in the grid if smaller items come up later
![eiAJk8.png](https://s2.ax1x.com/2019/07/22/eiAJk8.png)
> <strong>dense</strong> only changes the visual order of your items and might cause them to appear out of order, which is bad for accessibility.

Examples:

Consider this HTML:
![eiABmq.png](https://s2.ax1x.com/2019/07/22/eiABmq.png)
You define a grid with five columns and two rows, and set `grid-auto-flow` to `row` (which is also the default):
![eiAchF.png](https://s2.ax1x.com/2019/07/22/eiAchF.png)
When placing the items on the grid, you only specify spots for two of them:
![eiEC4S.png](https://s2.ax1x.com/2019/07/22/eiEC4S.png)

Because we set `grid-auto-flow` to `row`, our grid will look like this. Notice how the three items we didn't place (<strong>item-b</strong>, <strong>item-c</strong> and <strong>item-d</strong>) flow across the available rows:
![eiEDvd.png](https://s2.ax1x.com/2019/07/22/eiEDvd.png)

If we instead set `grid-auto-flow` to `column`, <strong>item-b</strong>, <strong>item-c</strong> and <strong>item-d</strong> flow down the columns:
![eiEv24.png](https://s2.ax1x.com/2019/07/22/eiEv24.png)
![eiVprR.png](https://s2.ax1x.com/2019/07/22/eiVprR.png)

###### grid
A shorthand for setting all of the following properties in a single declaration: `grid-template-rows`, `grid-template-columns`, `grid-template-areas`, `grid-auto-rows`, `grid-auto-columns`, and `grid-auto-flow`
> Note: You can only specify the explicit or the implicit grid properties in a single grid declaration

Values:
- <strong>none</strong> - sets all sub-properties to their initial values.
- <strong>&#60;grid-template&#62;</strong> - works the same as the grid-template shorthand.
- <strong>&#60;grid-template-rows&#62;</strong> / <strong>&#91; auto-flow && dense? &#93;</strong>	 <strong>&#60;grid-auto-columns&#62;?</strong> - sets grid-template-rows to the specified value. If the auto-flow keyword is to the right of the slash, it sets grid-auto-flow to column. If the dense keyword is specified additionally, the auto-placement algorithm uses a “dense” packing algorithm. If grid-auto-columns is omitted, it is set to auto.
- <strong>&#91; auto-flow && dense? &#93;</strong> <strong>&#60;grid-auto-rows&#62;</strong>? / <strong>&#60;grid-template-columns&#62;</strong> - sets grid-template-columns to the specified value. If the auto-flow keyword is to the left of the slash, it sets grid-auto-flow to row. If the dense keyword is specified additionally, the auto-placement algorithm uses a “dense” packing algorithm. If grid-auto-rows is omitted, it is set to auto.

Examples:

The following two code blocks are equivalent:
![eiMwjS.png](https://s2.ax1x.com/2019/07/22/eiMwjS.png)
The following two code blocks are equivalent:
![eiMyAs.png](https://s2.ax1x.com/2019/07/22/eiMyAs.png)
The following two code blocks are equivalent:
![eiQK5n.png](https://s2.ax1x.com/2019/07/22/eiQK5n.png)
And the following two code blocks are equivalent:
![eiQDxK.png](https://s2.ax1x.com/2019/07/22/eiQDxK.png)

It also accepts a more complex but quite handy syntax for setting everything at once. You specify grid-template-areas, grid-template-rows and grid-template-columns, and all the other sub-properties are set to their initial values. What you're doing is specifying the line names and track sizes inline with their respective grid areas. This is easiest to describe with an example:
![eiQoM8.png](https://s2.ax1x.com/2019/07/22/eiQoM8.png)
That's equivalent to this:
![eil9LF.png](https://s2.ax1x.com/2019/07/22/eil9LF.png)

#### Properties for the Children(Grid Items)
> Note: `float`, `display: inline-block`, `display: table-cell`, `vertical-align` and `column-*` properties have no effect on a grid item.

###### grid-column-start
###### grid-column-end
###### grid-row-start
###### grid-row-end
Determines a grid item's location within the grid by referring to specific grid lines. `grid-column-start`/`grid-row-start` is the line where the item begins, and `grid-column-end`/`grid-row-end` is the line where the item ends.

Values:
- <strong>&#60;line&#62;</strong> - can be a number to refer to a numbered grid line, or a name to refer to a named grid line
- <strong>span &#60;number&#62;</strong> - the item will span across the provided number of grid tracks
- <strong>span &#60;name&#62;</strong> - the item will span across until it hits the next line with the provided name
- <strong>auto</strong> - indicates auto-placement, an automatic span, or a default span of one
![eic9aj.png](https://s2.ax1x.com/2019/07/22/eic9aj.png)

Examples:
![eiceLF.png](https://s2.ax1x.com/2019/07/22/eiceLF.png)
![eicYLD.png](https://s2.ax1x.com/2019/07/22/eicYLD.png)

If no `grid-column-end`/`grid-row-end` is declared, the item will span 1 track by default.

Items can overlap each other. You can use `z-index` to control their stacking order.

###### grid-column
###### grid-row
Shorthand for `grid-column-start` + `grid-column-end`, and `grid-row-start` + `grid-row-end`, respectively.

Values:
- <strong>&#60;start-line&#62;</strong> / <strong>&#60;end-line&#62;</strong> - each one accepts all the same values as the longhand version, including span
![eigdnU.png](https://s2.ax1x.com/2019/07/22/eigdnU.png)

Example:
![eigo4A.png](https://s2.ax1x.com/2019/07/22/eigo4A.png)

If no end line value is declared, the item will span 1 track by default.

###### grid-area
Gives an item a name so that it can be referenced by a template created with the `grid-template-areas` property. Alternatively, this property can be used as an even shorter shorthand for `grid-row-start` + `grid-column-start` + `grid-row-end` + `grid-column-end`.

Values:
- <strong>&#60;name&#62;</strong> - a name of your choosing
- <strong>&#60;row-start&#62;</strong> / <strong>&#60;column-start&#62;</strong> / <strong>&#60;row-end&#62;</strong> / <strong>&#60;column-end&#62;</strong> - can be numbers or named lines
![ei2wxP.png](https://s2.ax1x.com/2019/07/22/ei2wxP.png)
Examples:

As a way to assign a name to the item:
![ei2c5j.png](https://s2.ax1x.com/2019/07/22/ei2c5j.png)
As the short-shorthand for `grid-row-start` + `grid-column-start` + `grid-row-end` + `grid-column-end`:
![ei2IqU.png](https://s2.ax1x.com/2019/07/22/ei2IqU.png)

###### justify-self
Aligns a grid item inside a cell along the <ins>inline (row) axis</ins> (as opposed to `align-self` which aligns along the <ins>block (column) axis</ins>). This value applies to a grid item inside a single cell.

Values:
- <strong>start</strong> - aligns the grid item to be flush with the start edge of the cell
- <strong>end</strong> - aligns the grid item to be flush with the end edge of the cell
- <strong>center</strong> - aligns the grid item in the center of the cell
- <strong>stretch</strong> - fills the whole width of the cell (this is the default)
![eiRpZD.png](https://s2.ax1x.com/2019/07/22/eiRpZD.png)

Examples:
![eiRAzt.png](https://s2.ax1x.com/2019/07/22/eiRAzt.png)
![eiRneS.png](https://s2.ax1x.com/2019/07/22/eiRneS.png)
![eiRlJs.png](https://s2.ax1x.com/2019/07/22/eiRlJs.png)
![eiRJyV.png](https://s2.ax1x.com/2019/07/22/eiRJyV.png)

To set alignment for all the items in a grid, this behavior can also be set on the grid container via the `justify-items` property.

###### align-self
Aligns a grid item inside a cell along the <ins>block (column) axis</ins> (as opposed to `justify-self` which aligns along the <ins>inline (row) axis</ins>). This value applies to the content inside a single grid item.

Values:
- <strong>start</strong> - aligns the grid item to be flush with the start edge of the cell
- <strong>end</strong> - aligns the grid item to be flush with the end edge of the cell
- <strong>center</strong> - aligns the grid item in the center of the cell
- <strong>stretch</strong> - fills the whole height of the cell (this is the default)
![eiRISI.png](https://s2.ax1x.com/2019/07/22/eiRISI.png)

Examples:
![eiRjYj.png](https://s2.ax1x.com/2019/07/22/eiRjYj.png)
![eiWF7F.png](https://s2.ax1x.com/2019/07/22/eiWF7F.png)
![eiWepR.png](https://s2.ax1x.com/2019/07/22/eiWepR.png)
![eiW3Ae.png](https://s2.ax1x.com/2019/07/22/eiW3Ae.png)

To align all the items in a grid, this behavior can also be set on the grid container via the `align-items` property.

###### place-self
`place-self` sets both the `align-self` and `justify-self` properties in a single declaration.

Values:
- <strong>auto</strong> - The “default” alignment for the layout mode.
- <strong>&#60;align-self&#62;</strong> / <strong>&#60;justify-self&#62;</strong> - The first value sets align-self, the second value justify-self. If the second value is omitted, the first value is assigned to both properties.

Examples:
![eiW2j0.png](https://s2.ax1x.com/2019/07/22/eiW2j0.png)
![eiW5EF.png](https://s2.ax1x.com/2019/07/22/eiW5EF.png)

All major browsers except Edge support the `place-self` shorthand property.
