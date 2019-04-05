---
layout: post
title: Code Splitting
subtitle: Webpack Guides 5学习笔记系列
date: 2019-04-05
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Webpack
---

- [Table of Contents](#table-of-contents)
  - [Preface](#preface)
  - [Entry Points](#entry-points)
  - [Prevent Duplication](#prevent-duplication)
  - [Dynamic Imports](#dynamic-imports)
  - [Prefetching/Preloading modules](#prefetchingpreloading-modules)

# Table of Contents

## Preface

`Code Splitting` allows you to <ins>split your code into various bundles</ins> which can then be **_loaded on demand_** or in parallel.

There are three general approaches to code splitting available:

1. Entry Points
   - Manually split code using entry configuration
2. Prevent Duplication
   - Use the `SplitChunksPlugin` to dedupe and split chunks
3. Dynamic Imports
   - Split code via inline function calls within modules

## Entry Points

## Prevent Duplication
The `SplitChunksPlugin` allows us to extract common dependencies into an existing entry chunk or an entirely new chunk. 
```javascript
const path = require('path');

  module.exports = {
    mode: 'development',
    entry: {
      index: './src/index.js',
      another: './src/another-module.js'
    },
    output: {
      filename: '[name].bundle.js',
      path: path.resolve(__dirname, 'dist')
    },
    optimization: {
      splitChunks: {
        chunks: 'all'
      }
    }
  };
```
 the `optimization.splitChunks` configuration option in place, we would see the duplicate dependency removed from entry points.


## Dynamic Imports

## Prefetching/Preloading modules
`webpack 4.6.0+` adds support for `prefetching` and `preloading`<br>
Using these inline directives while declaring your imports allows webpack to output “Resource Hint” which tells the browser that for:
1. preload
    - resource might be needed during the current navigation
2. prefetch
    - resource is probably needed for some navigation in the future

| Preload                                        | Prefetch                                       |
| ---------------------------------------------- | ---------------------------------------------- |
| starts loading in parallel to the parent chunk | starts after the parent chunk finishes loading |
| medium priority and is instantly downloaded    | downloaded while browser is idle               |
| instantly requested by the parent chunk        | used anytime in the future                     |
