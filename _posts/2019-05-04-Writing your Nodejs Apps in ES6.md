---
layout: post
title: Writing Your Node.js Apps Using ES6
subtitle: Nodejs Tricks
date: 2019-05-04
author: Jalever
header-img: img/post_light_bulb_bg.png
catalog: true
tags:
  - Node.js
---

## Dependencies
```js
npm i -D @babel/core @babel/node @babel/preset-env
```

## Package.json
```
"start": "nodemon --exec babel-node server.js"
```


## Building a `.babelrc` file
{
  "presets": [
    "@babel/preset-env"
  ]
}
