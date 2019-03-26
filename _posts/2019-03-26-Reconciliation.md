---
layout: post
title: Reconciliation
subtitle: React学习笔记系列
date: 2019-03-26
author: Jalever
header-img: img/post_2019_react_bg.png
catalog: true
tags:
  - React
---

- [Motivation](#motivation)
- [The Diffing Algorithm](#the-diffing-algorithm)
    - [Elements Of Different Types](#elements-of-different-types)
    - [DOM Elements Of The Same Type](#dom-elements-of-the-same-type)
    - [Component Elements Of The Same Type](#component-elements-of-the-same-type)
    - [Recursing On Children](#recursing-on-children)
    - [Keys](#keys)
- [Tradeoffs](#tradeoffs)

## Motivation
When you use `React`, at a single point in time you can think of the `render()` function as creating a tree of `React` elements. <br>
On the next state or props update, that `render()` function will return a different tree of `React` elements.<br>
the state of the art algorithms have a complexity in the order of `O(n3)` where `n` is the number of elements in the tree.

## The Diffing Algorithm
When diffing two trees, `React` first compares the two root elements. The behavior is different depending on the types of the root elements.

#### Elements Of Different Types
Whenever the root elements have different types, `React` will tear down the old tree and build the new tree from scratch. <br>
Going from `<a>` to `<img>`, or from `<Article>` to `<Comment>`, or from `<Button>` to `<div>` - any of those will lead to a full rebuild.<br>
When tearing down a tree, old DOM nodes are destroyed. Component instances receive `componentWillUnmount()`. <br>
When building up a new tree, new `DOM nodes` are inserted into the `DOM`. Component instances receive `componentWillMount()` and then `componentDidMount()`. Any state associated with the old tree is lost.<br>
Any components below the root will also get unmounted and have their state destroyed.<br>
For example, when diffing:
```js
<div>
  <Counter />
</div>

<span>
  <Counter />
</span>
```
This will destroy the old `Counter` and remount a new one.

#### DOM Elements Of The Same Type
When comparing two `React DOM elements` of the same type, React looks at the attributes of both, keeps the same underlying DOM node, and only updates the changed attributes.<br>
For example:
```js
<div className="before" title="stuff" />

<div className="after" title="stuff" />
```
By comparing these two elements, `React` knows to only modify the `className` on the underlying DOM node.


#### Component Elements Of The Same Type
When a component updates, the instance stays the same, so that state is maintained across renders. 
`React` updates the props of the underlying component instance to match the new element, and calls `componentWillReceiveProps()` and `componentWillUpdate()` on the underlying instance.
Next, the `render()` method is called and the diff algorithm recurses on the previous result and the new result.

#### Recursing On Children
By default, when recursing on the children of a `DOM node`, React just iterates over both lists of children at the same time and generates a mutation whenever there’s a difference.
For example, when adding an element at the end of the children, converting between these two trees works well:
```js
<ul>
  <li>first</li>
  <li>second</li>
</ul>

<ul>
  <li>first</li>
  <li>second</li>
  <li>third</li>
</ul>
```
`React` will match the two <li>first</li> trees, match the two `<li>second</li>` trees, and then insert the `<li>third</li>` tree.<br>
If you implement it naively, inserting an element at the beginning has worse performance.<br>
For example, converting between these two trees works poorly:<br>
```js
<ul>
  <li>Duke</li>
  <li>Villanova</li>
</ul>

<ul>
  <li>Connecticut</li>
  <li>Duke</li>
  <li>Villanova</li>
</ul>
```
`React` will mutate every child instead of realizing it can keep the `<li>Duke</li>` and `<li>Villanova</li>` subtrees intact.

#### Keys
In order to solve this issue, `React` supports a `key` attribute. <br>
When children have keys, `React` uses the key to match children in the original tree with children in the subsequent tree. <br>
When that’s not the case, you can add a new ID property to your model or hash some parts of the content to generate a key. <br>
<ins>***The key only has to be unique among its siblings, not globally unique***</ins><br>
Reorders can also cause issues with component state when ***indexes are used as keys***. <br>
Component instances are updated and reused based on their key. <br>
If the key is an index, moving an item changes it.<br> 
As a result, component state for things like uncontrolled inputs can get mixed up and updated in unexpected ways.<br>

## Tradeoffs
1. The algorithm will not try to match subtrees of different component types.
2. `Keys` should be stable, predictable, and unique. Unstable keys (like those produced by `Math.random()`) will cause many component instances and `DOM` nodes to be unnecessarily recreated, which can cause performance degradation and lost state in child components.