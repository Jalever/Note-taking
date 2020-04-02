---
layout: post
title: 重绘Repaint和回流(重排)Reflow
subtitle: Web Development系列
date: 2020-04-02
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - JavaScript
---

## 浏览器的渲染过程
![GGuwSH.png](https://s1.ax1x.com/2020/04/02/GGuwSH.png)
从上面这个图上，我们可以看到，浏览器渲染过程如下：

1. 解析`HTML`，生成`DOM`树，解析`CSS`，生成`CSSOM`树
2. 将`DOM`树和`CSSOM`树结合，生成渲染树(`Render Tree`)
3. `Layout`(回流):根据生成的渲染树，进行回流(`Layout`)，得到节点的几何信息（位置，大小）
4. `Painting`(重绘):根据渲染树以及回流得到的几何信息，得到节点的绝对像素
5. `Display`:将像素发送给`GPU`，展示在页面上。（这一步其实还有很多内容，比如会在GPU将多个合成层合并为同一个层，并展示在页面中。而`CSS3`硬件加速的原理则是新建合成层

## 重绘Repaint


## 回流Reflow

## 浏览器优化方法








