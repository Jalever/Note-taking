---
layout: post
title: Centering in CSS A Complete Guide
subtitle: CSS学习笔记系列
date: 2019-06-27
author: Jalever
header-img: img/css_bg_simple.png
catalog: true
tags:
  - CSS
---
- [Horizontal](#horizontal)
    - [Horizontal Level Element](#horizontal-level-element)
    - [Block Level Element](#block-level-element)
    - [Multiple Block Level Element](#multiple-block-level-element)

## Horizontal

#### Horizontal Level Element
You can center inline elements horizontally, within a block-level parent element, with just:

HTML Source Codes
```html
<header>
  This text is centered.
</header>

<nav role='navigation'>
  <a href="#0">One</a>
  <a href="#0">Two</a>
  <a href="#0">Three</a>
  <a href="#0">Four</a>
</nav>  
```

CSS Source Codes
```css
body {
  background: #f06d06;
}

header, nav {
  text-align: center;
  background: white;
  margin: 20px 0;
  padding: 10px;
}

nav a {
  text-decoration: none;
  background: #333;
  border-radius: 5px;
  color: white;
  padding: 3px 8px;
}
```

result
[![Zm4JQ1.md.png](https://s2.ax1x.com/2019/06/27/Zm4JQ1.md.png)](https://imgchr.com/i/Zm4JQ1)

This will work for inline, inline-block, inline-table, inline-flex, etc.


#### Block Level Element
You can center a block-level element by giving it `margin-left` and `margin-right` of `auto` (and it has a set `width`, otherwise it would be full width and wouldn't need centering). That's often done with shorthand like this:

HTML Source Codes
```html
<main>
  <div class="center">
    I'm a block level element and am centered.
  </div>
</main>
```

CSS Source Codes
```css
body {
  background: #f06d06;
}

main {
  background: white;
  margin: 20px 0;
  padding: 10px;
}

.center {
  margin: 0 auto;
  width: 200px;
  background: black;
  padding: 20px;
  color: white;
}
```

result
[![ZmIaPe.md.png](https://s2.ax1x.com/2019/06/27/ZmIaPe.md.png)](https://imgchr.com/i/ZmIaPe)

This will work no matter what the width of the block level element you're centering, or the parent.

#### Multiple Block Level Element
If you have two or more block-level elements that need to be centered horizontally in a row, chances are you'd be better served making them a different `display` type. Here's an example of making them `inline-block` and an example of flexbox:

HTML Source Codes
```html
<main class="inline-block-center">
  <div>
    I'm an element that is block-like with my siblings and we're centered in a row.
  </div>
  <div>
    I'm an element that is block-like with my siblings and we're centered in a row. I have more content in me than my siblings do.
  </div>
  <div>
    I'm an element that is block-like with my siblings and we're centered in a row.
  </div>
</main>

<main class="flex-center">
  <div>
    I'm an element that is block-like with my siblings and we're centered in a row.
  </div>
  <div>
    I'm an element that is block-like with my siblings and we're centered in a row. I have more content in me than my siblings do.
  </div>
  <div>
    I'm an element that is block-like with my siblings and we're centered in a row.
  </div>
</main>
```

CSS Source Codes
```css
body {
  background: #f06d06;
  font-size: 80%;
}

main {
  background: white;
  margin: 20px 0;
  padding: 10px;
}

main div {
  background: black;
  color: white;
  padding: 15px;
  max-width: 125px;
  margin: 5px;
}

.inline-block-center {
  text-align: center;
}
.inline-block-center div {
  display: inline-block;
  text-align: left;
}

.flex-center {
  display: flex;
  justify-content: center;
}
```

result
[![ZmTvHx.md.png](https://s2.ax1x.com/2019/06/27/ZmTvHx.md.png)](https://imgchr.com/i/ZmTvHx)

Unless you mean you have multiple block level elements stacked on top of each other, in which case the auto margin technique is still fine:

HTML Source Codes
```html
<main>
  <div>
    I'm an element that is block-like with my siblings and we're centered in a row.
  </div>
  <div>
    I'm an element that is block-like with my siblings and we're centered in a row. I have more content in me than my siblings do.
  </div>
  <div>
    I'm an element that is block-like with my siblings and we're centered in a row.
  </div>
</main>
```

CSS Source Codes
```css
body {
  background: #f06d06;
  font-size: 80%;
}

main {
  background: white;
  margin: 20px 0;
  padding: 10px;
}

main div {
  background: black;
  margin: 0 auto;
  color: white;
  padding: 15px;
  margin: 5px auto;
}

main div:nth-child(1) {
  width: 200px;
}
main div:nth-child(2) {
  width: 400px;
}
main div:nth-child(3) {
  width: 125px;
}
```

result
[![ZmqEr9.md.png](https://s2.ax1x.com/2019/06/27/ZmqEr9.md.png)](https://imgchr.com/i/ZmqEr9)
