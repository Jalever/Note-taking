---
layout: post
title: Store
subtitle: Redux学习笔记系列
date: 2019-04-03
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
  - Redux
---

In the previous sections, we defined the `actions` that ***represent the facts about “what happened”*** and the `reducers` that ***update the state according to those actions***.

The `store` has the following responsibilities:
- Holds application state
- Allows access to state via `getState()`
- Allows state to be updated via `dispatch(action)`
- Registers listeners via `subscribe(listener)`
- Handles unregistering of listeners via the function returned by `subscribe(listener).`

It's important to note that you'll only have a single store in a `Redux` application.<br>

It's easy to create a store if you have a reducer.<br>

In the previous section, we used `combineReducers()` to combine several reducers into one. We will now import it, and pass it to `createStore()`.<br>

```javascript
import { createStore } from 'redux';
import todoApp from './reducers';
const store = createStore(todoApp);
```

You may optionally specify the initial state as the second argument to `createStore()`.<br> 
This is useful for hydrating the state of the client to match the state of a `Redux` application running on the server.<br>
```javascript
const store = createStore(todoApp, window.STATE_FROM_SERVER)
```

## Dispatching Actions
```javascript
import {
  addTodo,
  toggleTodo,
  setVisibilityFilter,
  VisibilityFilters
} from './actions'

// Log the initial state
console.log(store.getState())

// Every time the state changes, log it
// Note that subscribe() returns a function for unregistering the listener
const unsubscribe = store.subscribe(() => console.log(store.getState()))

// Dispatch some actions
store.dispatch(addTodo('Learn about actions'))
store.dispatch(addTodo('Learn about reducers'))
store.dispatch(addTodo('Learn about store'))
store.dispatch(toggleTodo(0))
store.dispatch(toggleTodo(1))
store.dispatch(setVisibilityFilter(VisibilityFilters.SHOW_COMPLETED))

// Stop listening to state updates
unsubscribe()
```

## Source Code
```javascript
import { createStore } from 'redux'
import todoApp from './reducers'

const store = createStore(todoApp)
```


