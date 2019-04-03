---
layout: post
title: Data Flow
subtitle: Redux学习笔记系列
date: 2019-04-03
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
  - Redux
---

`Redux` architecture revolves around a strict unidirectional data flow.

This means that all data in an application follows the same lifecycle pattern, making the logic of your app more predictable and easier to understand.

The data lifecycle in any Redux app follows 4 steps:

## You call store.dispatch(action)

An action is a `plain object` describing what happened.<br>

## The `Redux` store calls the reducer function you gave it

The store will pass two arguments to the reducer: `the current state tree` and `the action`.<br>
Note that a `reducer` is a pure function.<br>
It only computes the next state.<br>
It should be completely predictable: calling it with the same inputs many times should produce the same outputs.<br>
It shouldn't perform any `side effects` like `API calls` or `router transitions`.


## The root reducer may combine the output of multiple reducers into a single state tree

## The Redux store saves the complete state tree returned by the root reducer
Every listener registered with `store.subscribe(listener)` will now be invoked;<br> 
listeners may call `store.getState()` to get the current state.