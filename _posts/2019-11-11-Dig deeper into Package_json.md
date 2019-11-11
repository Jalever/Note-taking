---
layout: post
title: Dig Deeper into Package.json
subtitle: Web Development
date: 2019-11-11
author: Jalever
header-img: img/post_2019_web_development_bg.png
catalog: true
tags:
    - Web Development
---

## dependencies
```text
npm install --save-dev
```
<strong>devDependencies</strong> are modules which are only required during development

The shorthand for saving a regular dependency is `-S` instead of `-D`: `npm i -S packagename`

Some good examples of dependencies which would be required at runtime include `React`, `Redux`, `Express`, and `Axios`.

---


## devDependencies
```text
npm install --save
```
<strong>dependencies</strong> are modules which are also required at runtime.

The shorthand for installing a devDependency is `npm i -D packagename`

Some good examples of when to install devDependencies would be `Nodemon`, `Babel`, `ESLint`, and testing frameworks like `Chai`, `Mocha`, `Enzyme`, etc…


## Package-lock.json
The package-lock specifies a `version`, `location` and `integrity hash for every module` and each of its dependencies, the install it creates will be the same, every single time
```js
"@babel/code-frame": {
  "version": "7.0.0",
  "resolved": "https://registry.npmjs.org/@babel/code-frame/-/code-frame-7.0.0.tgz",
  "integrity": "sha512-OfC2uemaknXr87bdLUkWog7nYuliM9Ij5HUcajsVcMCpQrcLmtxRbVFTIqmcSkSeYRBFBRxs2FiUqFJDLdiebA==",
  "dev": true,
  "requires": {
    "@babel/highlight": "^7.0.0"
  }
},
```









