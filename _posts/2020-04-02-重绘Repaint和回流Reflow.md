---
layout: post
title: 重绘Repaint和回流(重排)Reflow
subtitle: 重绘Repaint, 重排Reflow以及如何优化
date: 2020-04-02
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - JavaScript
---
- [浏览器的渲染过程](#%e6%b5%8f%e8%a7%88%e5%99%a8%e7%9a%84%e6%b8%b2%e6%9f%93%e8%bf%87%e7%a8%8b)
- [重绘Repaint](#%e9%87%8d%e7%bb%98repaint)
- [回流Reflow](#%e5%9b%9e%e6%b5%81reflow)
- [浏览器的优化机制](#%e6%b5%8f%e8%a7%88%e5%99%a8%e7%9a%84%e4%bc%98%e5%8c%96%e6%9c%ba%e5%88%b6)
- [减少重绘和重排](#%e5%87%8f%e5%b0%91%e9%87%8d%e7%bb%98%e5%92%8c%e9%87%8d%e6%8e%92)
    - [最小化重绘和重排](#%e6%9c%80%e5%b0%8f%e5%8c%96%e9%87%8d%e7%bb%98%e5%92%8c%e9%87%8d%e6%8e%92)
    - [批量修改DOM](#%e6%89%b9%e9%87%8f%e4%bf%ae%e6%94%b9dom)
    - [避免触发同步布局事件](#%e9%81%bf%e5%85%8d%e8%a7%a6%e5%8f%91%e5%90%8c%e6%ad%a5%e5%b8%83%e5%b1%80%e4%ba%8b%e4%bb%b6)

## 浏览器的渲染过程
![GGuwSH.png](https://s1.ax1x.com/2020/04/02/GGuwSH.png)
从上面这个图上，我们可以看到，浏览器渲染过程如下：

1. 解析`HTML`，生成`DOM`树，解析`CSS`，生成`CSSOM`树
2. 将`DOM`树和`CSSOM`树结合，生成渲染树(`Render Tree`)
3. `Layout`(回流):根据生成的渲染树，进行回流(`Layout`)，得到节点的几何信息（位置，大小）
4. `Painting`(重绘):根据渲染树以及回流得到的几何信息，得到节点的绝对像素
5. `Display`:将像素发送给`GPU`，展示在页面上。（这一步其实还有很多内容，比如会在GPU将多个合成层合并为同一个层，并展示在页面中。而`CSS3`硬件加速的原理则是新建合成层

## 重绘Repaint
由于节点的几何属性发生改变或者由于样式发生改变而不会影响布局的，称为<strong>重绘</strong>，例如`outline`, `visibility`, `color`、`background-color`等，重绘的代价是高昂的，因为浏览器必须验证DOM树上其他节点元素的可见性

## 回流Reflow
我们通过构造渲染树，我们将可见DOM节点以及它对应的样式结合起来，可是我们还需要计算它们在设备视口(viewport)内的确切位置和大小，这个计算的阶段就是<strong>回流</strong>

回流是影响浏览器性能的关键因素，因为其变化涉及到部分页面（或是整个页面）的布局更新. 一个元素的回流可能会导致了其所有子元素以及DOM中紧随其后的节点、祖先节点元素的随后的回流

## 浏览器的优化机制
现代的浏览器都是很聪明的，由于每次重排都会造成额外的计算消耗，因此大多数浏览器都会通过队列化修改并批量执行来优化重排过程。浏览器会将修改操作放入到队列里，直到过了一段时间或者操作达到了一个阈值，才清空队列。但是！当你获取布局信息的操作的时候，会强制队列刷新，比如当你访问以下属性或者使用以下方法:

- offsetTop、offsetLeft、offsetWidth、offsetHeight
- scrollTop、scrollLeft、scrollWidth、scrollHeight
- clientTop、clientLeft、clientWidth、clientHeight
- getComputedStyle()
- getBoundingClientRect

以上属性和方法都需要返回最新的布局信息，因此浏览器不得不清空队列，触发回流重绘来返回正确的值。因此，我们在修改样式的时候，**最好避免使用上面列出的属性，他们都会刷新渲染队列** 如果要使用它们，最好将值缓存起来

## 减少重绘和重排

#### 最小化重绘和重排
由于重绘和重排可能代价比较昂贵，因此最好就是可以减少它的发生次数。为了减少发生次数，我们可以合并多次对DOM和样式的修改，然后一次处理掉。考虑这个例子
```js
const el = document.getElementById('test');
el.style.padding = '5px';
el.style.borderLeft = '1px';
el.style.borderRight = '2px';
```
例子中，有三个样式属性被修改了，每一个都会影响元素的几何结构，引起回流。当然，大部分现代浏览器都对其做了优化，因此，只会触发一次重排。但是如果在旧版的浏览器或者在上面代码执行的时候，有其他代码访问了布局信息(上文中的会触发回流的布局信息)，那么就会导致三次重排。

因此，我们可以合并所有的改变然后依次处理，比如我们可以采取以下的方式:
- 使用cssText
```js
const el = document.getElementById('test');
el.style.cssText += 'border-left: 1px; border-right: 2px; padding: 5px;';
```

- 修改CSS的class
```js
const el = document.getElementById('test');
el.className += ' active';
```

#### 批量修改DOM
当我们需要对DOM对一系列修改的时候，可以通过以下步骤减少回流重绘次数：

1. 使元素脱离文档流
2. 对其进行多次修改
3. 将元素带回到文档中

该过程的第一步和第三步可能会引起回流，但是经过第一步之后，对DOM的所有修改都不会引起回流重绘，因为它已经不在渲染树了

有三种方式可以让DOM脱离文档流:
- 隐藏元素，应用修改，重新显示
- 使用文档片段(document fragment)在当前DOM之外构建一个子树，再把它拷贝回文档。
- 将原始元素拷贝到一个脱离文档的节点中，修改节点后，再替换原始的元素

考虑我们要执行一段批量插入节点的代码:
```js
function appendDataToElement(appendToElement, data) {
    let li;
    for (let i = 0; i < data.length; i++) {
    	li = document.createElement('li');
        li.textContent = 'text';
        appendToElement.appendChild(li);
    }
}

const ul = document.getElementById('list');
appendDataToElement(ul, data);
```

如果我们直接这样执行的话，由于每次循环都会插入一个新的节点，会导致浏览器回流一次

我们可以使用上述的三种方式进行优化:

<strong>隐藏元素，应用修改，重新显示</strong><br/>
这个会在展示和隐藏节点的时候，产生两次回流

```js
function appendDataToElement(appendToElement, data) {
    let li;
    for (let i = 0; i < data.length; i++) {
    	li = document.createElement('li');
        li.textContent = 'text';
        appendToElement.appendChild(li);
    }
}
const ul = document.getElementById('list');
ul.style.display = 'none';
appendDataToElement(ul, data);
ul.style.display = 'block';
```

<strong>使用文档片段(document fragment)在当前DOM之外构建一个子树，再把它拷贝回文档</strong><br/>

```js
const ul = document.getElementById('list');
const fragment = document.createDocumentFragment();
appendDataToElement(fragment, data);
ul.appendChild(fragment);
```

<strong>将原始元素拷贝到一个脱离文档的节点中，修改节点后，再替换原始的元素</strong><br/>

```js
const ul = document.getElementById('list');
const clone = ul.cloneNode(true);
appendDataToElement(clone, data);
ul.parentNode.replaceChild(clone, ul);
```

#### 避免触发同步布局事件
上文我们说过，当我们访问元素的一些属性的时候，会导致浏览器强制清空队列，进行强制同步布局。举个例子，比如说我们想将一个p标签数组的宽度赋值为一个元素的宽度，我们可能写出这样的代码：
```js
function initP() {
    for (let i = 0; i < paragraphs.length; i++) {
        paragraphs[i].style.width = box.offsetWidth + 'px';
    }
}
```

这段代码看上去是没有什么问题，可是其实会造成很大的性能问题。在每次循环的时候，都读取了box的一个`offsetWidth`属性值，然后利用它来更新p标签的width属性。这就导致了每一次循环的时候，浏览器都必须先使上一次循环中的样式更新操作生效，才能响应本次循环的样式读取操作。每一次循环都会强制浏览器刷新队列。我们可以优化为:

```js
const width = box.offsetWidth;
function initP() {
    for (let i = 0; i < paragraphs.length; i++) {
        paragraphs[i].style.width = width + 'px';
    }
}
```
