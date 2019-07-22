---
layout: post
title: Margin Collapse
subtitle: Web Development
date: 2019-04-01
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Web Development
  - CSS
---

In this next example, I have a div with a background color of grey.<br>
This div has two paragraphs inside it. <br>
The outer div element has a margin-bottom of 40 pixels; <br>
the paragraphs also have a top and bottom margin of 20 pixels.

```javascript
.outer {
   background-color: #ccc;
  margin: 0 0 40px 0;
}

p {
  padding: 0;
  margin: 20px 0 20px 0;
  background-color: rgb(233,78,119);
  color: #fff;
}
```

As there is nothing between the margin of the `p` element and the margin on the outer div, the two will collapse and so the paragraphs end up flush with the top and bottom of the box. <br>
We don’t see any grey above and below the paragraphs.
