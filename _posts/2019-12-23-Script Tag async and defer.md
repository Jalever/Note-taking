---
layout: post
title: Script Tag - Async and Defer
subtitle: Web Development
date: 2019-12-23
author: Jalever
header-img: img/post_2019_web_development_bg.png
catalog: true
tags:
    - Web Development
---

In HTML5, you can tell browser when to run your JavaScript code. There are 3 possibilities:
```
<script       src="myscript.js"></script>

<script async src="myscript.js"></script>

<script defer src="myscript.js"></script>
```

1. Without `async` or `defer`, browser will run your script immediately, before rendering the elements that's below your script tag.
2. With `async` (asynchronous), browser will continue to <strong>load</strong> the HTML page and <strong>render</strong> it while the browser load and execute the script at the same time.
3. With `defer`, browser will run your script when the page <strong>finished parsing</strong>. (not necessary finishing downloading all image files. This is good.)





