---
layout: post
title: Repaint and Reflow
subtitle: Web Development
date: 2019-03-27
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Web Development
---

- [Preface](#preface)
- [Reflow[回流/重排]](#reflow%E5%9B%9E%E6%B5%81%E9%87%8D%E6%8E%92)
    - [导致回流的操作](#%E5%AF%BC%E8%87%B4%E5%9B%9E%E6%B5%81%E7%9A%84%E6%93%8D%E4%BD%9C)
    - [导致回流的属性和方法](#%E5%AF%BC%E8%87%B4%E5%9B%9E%E6%B5%81%E7%9A%84%E5%B1%9E%E6%80%A7%E5%92%8C%E6%96%B9%E6%B3%95)
- [Repaint[重绘]](#repaint%E9%87%8D%E7%BB%98)

## Preface

1. 浏览器使用`流式布局模型` (Flow Based Layout)
2. 浏览器会把`HTML`解析成`DOM`，把`CSS`解析成`CSSOM`，`DOM`和`CSSOM`合并就产生了`Render Tree`
3. 有了`RenderTree`，我们就知道了所有节点的样式，然后计算他们在页面上的大小和位置，最后把节点绘制到页面上
4. 由于浏览器使用流式布局，对`Render Tree`的计算通常只需要遍历一次就可以完成，但`table`及其内部元素除外，他们可能需要多次计算，通常要花 3 倍于同等元素的时间，这也是为什么要避免使用`table`布局的原因之一

当DOM的变化影响了元素的几何属性（宽或高），浏览器需要重新计算元素的几何属性，同样其他元素的几何属性和位置也会因此受到影响。浏览器会使渲染树中受到影响的部分失效，并重新构造渲染树。这个过程称为`重排`。完成重排后，浏览器会重新绘制受影响的部分到屏幕，该过程称为`重绘`
> Reflow 必将引起 Repaint，Repaint 不一定会引起 Reflow


## Reflow[回流/重排]

当`Render Tree`中部分或全部元素的**_尺寸_**、**_结构_**、或**_某些属性_**发生改变时，浏览器重新渲染部分或全部文档的过程称为`回流`

#### 导致回流的操作
- 页面首次渲染
- 浏览器窗口大小发生改变
- 元素尺寸或位置发生改变
- 元素内容变化（文字数量或图片大小等等）
- 元素字体大小变化
- 添加或者删除可见的DOM元素
- 激活`CSS`伪类（例如：`:hover`）
- 查询某些属性或调用某些方法

#### 导致回流的属性和方法
- clientWidth
- clientHeight
- clientTop
- clientLeft
- offsetWidth
- offsetHeight
- offsetTop
- offsetLeft
- scrollWidth
- scrollHeight
- scrollTop
- scrollLeft
- scrollIntoView()
- scrollIntoViewIfNeeded()
- getComputedStyle()
- getBoundingClientRect()
- scrollTo()

## Repaint[重绘]

当页面中元素样式的改变并不影响它在文档流中的位置时（例如：**_color_**、**_background-color_**、**_visibility_**等），浏览器会将新样式赋予给元素并重新绘制它，这个过程称为`重绘`
