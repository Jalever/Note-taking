---
layout: post
title: Code Splitting
subtitle: React Router Guides学习笔记系列 4
date: 2019-04-09
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
  - React Router
---

- `webpack `
- `@babel/plugin-syntax-dynamic-import`
- `loadable-components`

`.babelrc` should look something like this:
```javascript
{
  "presets": ["@babel/preset-react"],
  "plugins": ["@babel/plugin-syntax-dynamic-import"]
}

```

`webpack` has built-in support for dynamic imports<br>
if you are using `Babel` (e.g., to compile `JSX` to `JavaScript`) then you will need to use the `@babel/plugin-syntax-dynamic-import` plugin.<br> 
This is a syntax-only plugin, meaning `Babel` won’t do any additional transformations. <br>
The plugin simply allows `Babel` to parse dynamic imports so `webpack` can bundle them as a code split.

`loadable-components` is a library for loading components with dynamic imports. It handles all sorts of edge cases automatically and makes code splitting simple! 

```javascript
import loadable from '@loadable/component'
import Loading from "./Loading";

const LoadableComponent = loadable(() => import('./Dashboard'), {
  fallback: Loading,
})

export default class LoadableDashboard extends React.Component {
  render() {
    return <LoadableComponent />;
  }
}

```


