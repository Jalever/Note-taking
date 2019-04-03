---
layout: post
title: Actions
subtitle: React Redux学习笔记系列
date: 2019-04-03
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
  - React Redux
---

- [Action](#action)
- [Action Creators](#action-creators)
- [Example](#example)

## Action
`Actions` are payloads of information that send data from your application to your store.
They are the only source of information for the store.
You send them to the store using `store.dispatch()`.
`Actions` are plain JavaScript objects.
`Actions` must have a type property that indicates the type of action being performed. Types should typically be defined as ***string constants***.
```javascript
{
  type: TOGGLE_TODO,
  index: 5
}
```

## Action Creators
Action creators are exactly that—functions that create actions. 
In `Redux`, action creators simply return an action
```javascript
function addTodo(text) {
  return {
    type: ADD_TODO,
    text
  }
}
```

In `react-redux`'s `connect()`, you can use `bindActionCreators()` to automatically bind many action creators to a `dispatch()` function.


## Example
```javascript
/*
 * action types
 */

export const ADD_TODO = 'ADD_TODO'
export const TOGGLE_TODO = 'TOGGLE_TODO'
export const SET_VISIBILITY_FILTER = 'SET_VISIBILITY_FILTER'

/*
 * other constants
 */

export const VisibilityFilters = {
  SHOW_ALL: 'SHOW_ALL',
  SHOW_COMPLETED: 'SHOW_COMPLETED',
  SHOW_ACTIVE: 'SHOW_ACTIVE'
}

/*
 * action creators
 */

export function addTodo(text) {
  return { type: ADD_TODO, text }
}

export function toggleTodo(index) {
  return { type: TOGGLE_TODO, index }
}

export function setVisibilityFilter(filter) {
  return { type: SET_VISIBILITY_FILTER, filter }
}
```