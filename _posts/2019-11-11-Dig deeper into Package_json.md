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












