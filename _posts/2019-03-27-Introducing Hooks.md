---
layout: post
title: Introducing Hooks
subtitle: React Hooks学习笔记系列 1
date: 2019-03-27
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
  - React Hooks
---

`Hooks` let you use `state` and `other React features` without writing a `class`.

```javascript
import React, { useState } from "react";

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

- [No Breaking Changes](#no-breaking-changes)
- [Motivation](#motivation)
    - [It’s hard to reuse stateful logic between components](#its-hard-to-reuse-stateful-logic-between-components)
    - [Complex components become hard to understand](#complex-components-become-hard-to-understand)
    - [Classes confuse both people and machines](#classes-confuse-both-people-and-machines)
- [Gradual Adoption Strategy](#gradual-adoption-strategy)
- [Hooks Tutorial](#hooks-tutorial)

## No Breaking Changes
- Completely opt-in
  - You can try `Hooks` in a few components without rewriting any existing code.But you don’t have to learn or use `Hooks` right now if you don’t want to.
- 100% backwards-compatible
  - `Hooks` don’t contain any breaking changes.
- Available now
  - `Hooks` are now available with the release of `v16.8.0`.

## Motivation

#### It’s hard to reuse stateful logic between components
`React` doesn’t offer a way to “attach” reusable behavior to a component (for example, connecting it to a store).<br>
With `Hooks`, you can extract stateful logic from a component so it can be tested independently and reused.<br> 
`Hooks` allow you to reuse stateful logic without changing your component hierarchy. <br>
This makes it easy to share `Hooks` among many components or with the community.

#### Complex components become hard to understand
We’ve often had to maintain components that each lifecycle method contains a mix of unrelated logic.
`Hooks` let you ***split one component into smaller functions based on what pieces are related*** (such as ***setting up a subscription*** or ***fetching data***), rather than forcing a split based on lifecycle methods. <br>
You may also opt into managing the component’s local state with a reducer to make it more predictable.

#### Classes confuse both people and machines
We’ve found that `classes` can be a large barrier to learning `React`. You have to understand how `this` works in `JavaScript`.<br>
`Hooks` let you use more of `React`’s features without classes. 

## Gradual Adoption Strategy
`Hooks` work side-by-side with existing code so you can adopt them gradually. 

## Hooks Tutorial
1. Introducing Hooks
2. [Hooks at a Glance](https://jalever.github.io/2019/03/27/Hooks-at-a-Glance/)