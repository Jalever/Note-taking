---
layout: post
title: Web Component
subtitle: React学习笔记系列
date: 2019-03-26
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
---

`React` and `Web Components` are built to solve different problems. <br>
`Web Components` provide strong encapsulation for reusable components, while `React` provides a declarative library that keeps the `DOM` in sync with your data. <br>
The two goals are complementary.<br>
As a developer, you are free to use `React` in your `Web Components`, or to use `Web Components` in `React`, or both.

## Using Web Components in React
> `Web Components` often expose an imperative `API`. 
> For instance, a `video Web Component` might expose `play()` and `pause()` functions. 
> To access the imperative APIs of a Web Component, you will need to use a `ref` to interact with the `DOM` node directly. 
> If you are using `third-party Web Components`, the best solution is to write a `React` component that behaves as a wrapper for your `Web Component`.
> Events emitted by a `Web Component` may not properly propagate through a `React render tree`. 
> You will need to manually attach event handlers to handle these events within your `React` components.

One common confusion is that Web Components use `class` instead of `className`.
```javascript
function BrickFlipbox() {
  return (
    <brick-flipbox class="demo">
      <div>front</div>
      <div>back</div>
    </brick-flipbox>
  );
}
```

## Using React in your Web Components
```javascript
class XSearch extends HTMLElement {
  connectedCallback() {
    const mountPoint = document.createElement('span');
    this.attachShadow({ mode: 'open' }).appendChild(mountPoint);

    const name = this.getAttribute('name');
    const url = 'https://www.google.com/search?q=' + encodeURIComponent(name);
    ReactDOM.render(<a href={url}>{name}</a>, mountPoint);
  }
}
customElements.define('x-search', XSearch);
```