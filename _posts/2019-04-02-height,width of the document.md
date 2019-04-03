---
layout: post
title: Height / Width of the Document
subtitle: Web Development学习笔记系列
date: 2019-04-02
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Web Development
---

- [document.body.scrollHeight](#documentbodyscrollheight)
- [document.body.offsetHeight](#documentbodyoffsetheight)
- [document.body.clientHeight](#documentbodyclientheight)
- [window.innerWidth/Height](#windowinnerwidthheight)

## document.body.scrollHeight

## document.body.offsetHeight
content, padding, border

## document.body.clientHeight
Properties clientWidth/clientHeight of document.documentElement is exactly what we want here
If there’s a scrollbar, and it occupies some space, then these two lines show different values:
```javascript
alert( window.innerWidth ); // full window width
alert( document.documentElement.clientWidth ); // window width minus the scrollbar
```

## window.innerWidth/Height