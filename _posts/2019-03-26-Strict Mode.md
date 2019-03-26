---
layout: post
title: Strict Mode
subtitle: React学习笔记系列
date: 2019-03-26
author: Jalever
header-img: img/post_2019_react_bg.jpg
catalog: true
tags:
  - React
---

`StrictMode` is a tool for highlighting potential problems in an application.
Like <ins>***Fragment***</ins>, `StrictMode` does not render any visible UI.
It activates additional checks and warnings for its descendants.
You can enable strict mode for any part of your application. 

> Note: Strict mode checks are run in development mode only; they do not impact the production build.

For example: 
```javascript


import React from 'react';

function ExampleApplication() {
  return (
    <div>
      <Header />
      <React.StrictMode>
        <div>
          <ComponentOne />
          <ComponentTwo />
        </div>
      </React.StrictMode>
      <Footer />
    </div>
  );
}
```
In the above example, strict mode checks will not be run against the `Header` and `Footer` components. However, `ComponentOne` and `ComponentTwo`, as well as all of their descendants, will have the checks.

`StrictMode` currently helps with:
- [Identifying components with unsafe lifecycles](#identifying-components-with-unsafe-lifecycles)
- [Warning about legacy string ref API usage](#warning-about-legacy-string-ref-api-usage)
- [Warning about deprecated findDOMNode usage](#warning-about-deprecated-finddomnode-usage)
- [Detecting unexpected side effects](#detecting-unexpected-side-effects)
- [Detecting legacy context API](#detecting-legacy-context-api)

## Identifying components with unsafe lifecycles
Certain legacy lifecycle methods are unsafe for use in async `React` applications. <br>
If your application uses third party libraries, it can be difficult to ensure that these lifecycles aren’t being used. <br>
Fortunately, `strict mode` can help with this! <br>

## Warning about legacy string ref API usage
Previously, React provided two ways for managing refs: the legacy `string ref API` and `the callback API`. 
```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);

    this.inputRef = React.createRef();
  }

  render() {
    return <input type="text" ref={this.inputRef} />;
  }

  componentDidMount() {
    this.inputRef.current.focus();
  }
}
```
Since `object refs` were largely added as a replacement for `string refs`, `strict mode` now warns about usage of `string refs`.

## Warning about deprecated findDOMNode usage
React used to support `findDOMNode` to search the tree for a `DOM` node given a class instance. Normally you don’t need this because you can attach a ref directly to a `DOM` node.

## Detecting unexpected side effects
Conceptually, `React` does work in two phases:
- The <ins>***render phase***</ins> determines what changes need to be made to e.g. the DOM. During this phase, `React` calls render and then compares the result to the previous render.
- The <ins>***commit phase***</ins> is when `React` applies any changes. (In the case of `React DOM`, this is when `React` inserts, updates, and removes DOM nodes.) `React` also calls lifecycles like `componentDidMount` and `componentDidUpdate` during this phase.
The `commit phase` is usually very fast, but rendering can be slow. For this reason, the upcoming async mode (which is not enabled by default yet) breaks the rendering work into pieces, pausing and resuming the work to avoid blocking the browser. This means that `React` may invoke `render phase` lifecycles more than once before committing, or it may invoke them without committing at all (because of an error or a higher priority interruption).<br>
`Render phase` lifecycles include the following class component methods:
- constructor
- componentWillMount
- componentWillReceiveProps
- componentWillUpdate
- getDerivedStateFromProps
- shouldComponentUpdate
- setState(updater [,callback]) updater functions ( the first argument )
Because the above methods might be called more than once, it’s important that they do not contain side-effects. Ignoring this rule can lead to a variety of problems, including `memory leaks` and `invalid application state`. Unfortunately, it can be difficult to detect these problems as they can often be non-deterministic.
`Strict mode` can’t automatically detect side effects for you, but it can help you spot them by making them a little more deterministic. <br/>
This is done by intentionally double-invoking the following methods:
- Class component constructor method
- The render method
- setState updater functions (the first argument)
- The static getDerivedStateFromProps lifecycle

> This only applies to development mode. Lifecycles will not be double-invoked in production mode.

## Detecting legacy context API
The legacy `context API` is error-prone, and will be removed in a future major version.


