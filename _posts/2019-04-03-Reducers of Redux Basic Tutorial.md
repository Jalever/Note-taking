---
layout: post
title: (Redux)Reducers
subtitle: Redux
date: 2019-04-03
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
---

`Reducers` specify how the application's state changes in response to actions sent to the store.

Remember that actions only describe what happened, but don't describe how the application's state changes.

## Designing the State Shape
In `Redux`, all the application state is stored as a single object.

## Handling Actions
The `reducer` is a ***pure function*** that takes the ***previous state*** and an ***action***, and returns the ***next state***.
```javascript
(previousState, action) => newState
```
Given the same arguments, it should calculate the next state and return it. <br>
No surprises. <br>
No side effects. <br>
No API calls. <br>
No mutations. <br>
Just a calculation

Things you should never do inside a reducer:
- Mutate its arguments
- Perform side effects like `API calls` and `routing transitions`
- Call non-pure functions, e.g. `Date.now()` or `Math.random()`


## Handling More Actions
```javascript
import {
  ADD_TODO,
  TOGGLE_TODO,
  SET_VISIBILITY_FILTER,
  VisibilityFilters
} from './actions'

...

function todoApp(state = initialState, action) {
  switch (action.type) {
    case SET_VISIBILITY_FILTER:
      return Object.assign({}, state, {
        visibilityFilter: action.filter
      })
    case ADD_TODO:
      return Object.assign({}, state, {
        todos: [
          ...state.todos,
          {
            text: action.text,
            completed: false
          }
        ]
      })
    default:
      return state
  }
}
```

## Splitting Reducers
```javascript
function todos(state = [], action) {
  switch (action.type) {
    case ADD_TODO:
      return [
        ...state,
        {
          text: action.text,
          completed: false
        }
      ]
    case TOGGLE_TODO:
      return state.map((todo, index) => {
        if (index === action.index) {
          return Object.assign({}, todo, {
            completed: !todo.completed
          })
        }
        return todo
      })
    default:
      return state
  }
}

function visibilityFilter(state = SHOW_ALL, action) {
  switch (action.type) {
    case SET_VISIBILITY_FILTER:
      return action.filter
    default:
      return state
  }
}

function todoApp(state = {}, action) {
  return {
    visibilityFilter: visibilityFilter(state.visibilityFilter, action),
    todos: todos(state.todos, action)
  }
}
```
Note that each of these reducers is managing its own part of the global state.<br>
The state parameter is different for every reducer, and corresponds to the part of the state it manages.<br>
Redux provides a utility called `combineReducers()` that does the same boilerplate logic that the todoApp above currently does.
All `combineReducers()` does is generate a function that calls your reducers with the slices of state selected according to their keys, and combines their results into a single object again.
`combineReducers()` does not create a new object if all of the reducers provided to it do not change state.

## Source Code
```javascript
import { combineReducers } from 'redux'
import {
  ADD_TODO,
  TOGGLE_TODO,
  SET_VISIBILITY_FILTER,
  VisibilityFilters
} from './actions'
const { SHOW_ALL } = VisibilityFilters

function visibilityFilter(state = SHOW_ALL, action) {
  switch (action.type) {
    case SET_VISIBILITY_FILTER:
      return action.filter
    default:
      return state
  }
}

function todos(state = [], action) {
  switch (action.type) {
    case ADD_TODO:
      return [
        ...state,
        {
          text: action.text,
          completed: false
        }
      ]
    case TOGGLE_TODO:
      return state.map((todo, index) => {
        if (index === action.index) {
          return Object.assign({}, todo, {
            completed: !todo.completed
          })
        }
        return todo
      })
    default:
      return state
  }
}

const todoApp = combineReducers({
  visibilityFilter,
  todos
})

export default todoApp
```
