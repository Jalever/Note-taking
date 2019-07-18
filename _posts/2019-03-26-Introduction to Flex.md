---
layout: post
title: Introduction to Flex
subtitle: Aligning Items in a Flex Container
date: 2019-03-26
author: Jalever
header-img: img/css_bg_simple.png
catalog: true
tags:
  - CSS
---

- [Overview](#overview)
- [Parent Element(Container)](#parent-elementcontainer)
    - [flex-direction](#flex-direction)
    - [flex-wrap](#flex-wrap)
    - [flex-flow](#flex-flow)
    - [justify-content](#justify-content)
    - [align-items](#align-items)
    - [align-content](#align-content)
- [Child Elements(Items)](#child-elementsitems)
    - [Order](#order)
    - [flex-grow](#flex-grow)
    - [flex-shrink](#flex-shrink)
    - [flex-basis](#flex-basis)
    - [flex](#flex)
    - [align-self](#align-self)

## Overview
One of the reasons that flexbox quickly caught the interest of web developers is that it brought proper alignment capabilities to the web for the first time. It enabled proper vertical alignment, so we can at last easily center a box. In this guide, we will take a thorough look at how the alignment and justification properties work in Flexbox.

To center our box we use the <strong>align-items</strong> property to align our item on the cross axis, which in this case is the block axis running vertically. We use <strong>justify-content</strong> to align the item on the main axis, which in this case the inline axis running horizontally.
![ZLK7M8.png](https://s2.ax1x.com/2019/07/17/ZLK7M8.png)

The <strong>Flex</strong> CSS property sets how a flex item will grow or shrink to fit the space available in its flex container. It is a shorthand for `flex-grow`, `flex-shrink`, and `flex-basis`.


## Parent Element(Container)
The <strong>Flex Container</strong> properties are:
- flex-direction
- flex-wrap
- flex-flow
- justify-content
- align-items
- align-content

#### flex-direction
The <strong>flex-direction</strong> CSS property sets how flex items are placed in the flex container defining the main axis and the direction (normal or reversed).

###### Formal Syntax
![ZqhkSs.png](https://s2.ax1x.com/2019/07/17/ZqhkSs.png)
![Zq4Lrt.png](https://s2.ax1x.com/2019/07/17/Zq4Lrt.png)

#### flex-wrap
The <strong>flex-wrap</strong> CSS property sets whether flex items are forced onto one line or can wrap onto multiple lines. If wrapping is allowed, it sets the direction that lines are stacked.

###### Formal Syntax
![Zq5hyn.png](https://s2.ax1x.com/2019/07/17/Zq5hyn.png)
![ZqIVOI.png](https://s2.ax1x.com/2019/07/17/ZqIVOI.png)

#### flex-flow
The <strong>flex-flow</strong> CSS property is a shorthand property for `flex-direction` and `flex-wrap` properties.

###### Formal Syntax
![ZqID1J.png](https://s2.ax1x.com/2019/07/17/ZqID1J.png)
![ZqoZ34.png](https://s2.ax1x.com/2019/07/17/ZqoZ34.png)

#### justify-content
The CSS <strong>justify-content</strong> property defines how the browser distributes space between and around content items along the <ins>main-axis</ins> of a flex container, and the inline axis of a grid container.

###### Formal Syntax
![ZqTXlQ.png](https://s2.ax1x.com/2019/07/17/ZqTXlQ.png)
![Zq7WNV.png](https://s2.ax1x.com/2019/07/17/Zq7WNV.png)

#### align-items
The CSS <strong>align-items</strong> property sets the `align-self` value on all direct children as a group. In Flexbox, it controls the alignment of items on the <ins>Cross Axis</ins>.

###### Formal Syntax
![ZqHWqA.png](https://s2.ax1x.com/2019/07/17/ZqHWqA.png)
![ZqH4at.png](https://s2.ax1x.com/2019/07/17/ZqH4at.png)
![ZqHTG8.png](https://s2.ax1x.com/2019/07/17/ZqHTG8.png)
![ZqHHxg.png](https://s2.ax1x.com/2019/07/17/ZqHHxg.png)


#### align-content
So far we have been aligning the items, or an individual item inside the area defined by the flex-container. If you have a wrapped multiple-line flex container then you might also want to use the <strong>align-content</strong> property to control the distribution of space between the rows. In the specification this is described as <ins>Packing Flex Lines</ins>.



###### Formal Syntax
![Zqq8cF.png](https://s2.ax1x.com/2019/07/17/Zqq8cF.png)
![ZqqYnJ.png](https://s2.ax1x.com/2019/07/17/ZqqYnJ.png)
![ZqqtB9.png](https://s2.ax1x.com/2019/07/17/ZqqtB9.png)
![ZqqN7R.png](https://s2.ax1x.com/2019/07/17/ZqqN7R.png)

###### Example
![ZLQNN9.png](https://s2.ax1x.com/2019/07/17/ZLQNN9.png)
![ZLQlcV.png](https://s2.ax1x.com/2019/07/17/ZLQlcV.png)

## Child Elements(Items)
The <strong>Flex item</strong> properties are:
- order
- flex-grow
- flex-shrink
- flex-basis
- flex
- align-self

#### Order
The <strong>order</strong> CSS property sets the order to lay out an item in a flex container. Items in a container are sorted by ascending order value and then by their source code order.

The order value must be a number, default value is `0`.
![ZLVaEq.png](https://s2.ax1x.com/2019/07/17/ZLVaEq.png)
![ZLVBCT.png](https://s2.ax1x.com/2019/07/17/ZLVBCT.png)

#### flex-grow
The <strong>flex-grow</strong> property specifies how much a flex item will grow relative to the rest of the flex items.

The value must be a number, default value is `0`.
![ZLVzRS.png](https://s2.ax1x.com/2019/07/17/ZLVzRS.png)
![ZLZSxg.png](https://s2.ax1x.com/2019/07/17/ZLZSxg.png)

#### flex-shrink
The <strong>flex-shrink</strong> CSS property sets the flex shrink factor of a flex item. If the size of all flex items is larger than the flex container, items shrink to fit according to <strong>flex-shrink</strong>.

The value must be a number, default value is `1`.
![ZLmf5q.png](https://s2.ax1x.com/2019/07/17/ZLmf5q.png)
![ZLmI2T.png](https://s2.ax1x.com/2019/07/17/ZLmI2T.png)
![ZLmbqJ.png](https://s2.ax1x.com/2019/07/17/ZLmbqJ.png)
![ZLmOaR.png](https://s2.ax1x.com/2019/07/17/ZLmOaR.png)
![ZLmLZ9.png](https://s2.ax1x.com/2019/07/17/ZLmLZ9.png)

#### flex-basis
The <strong>flex-basis</strong> property specifies the initial length of a flex item.

![ZLuF6U.png](https://s2.ax1x.com/2019/07/17/ZLuF6U.png)
![ZLunt1.png](https://s2.ax1x.com/2019/07/17/ZLunt1.png)

#### flex
The <strong>flex</strong> property is a shorthand property for the `flex-grow`, `flex-shrink`, and `flex-basis` properties.

#### align-self
The <strong>align-self</strong> property specifies the alignment for the selected item inside the flexible container.

The <strong>align-self</strong> property overrides the default alignment set by the container's <strong>align-items</strong> property.
![ZLuO9x.png](https://s2.ax1x.com/2019/07/17/ZLuO9x.png)
