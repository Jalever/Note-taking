---
layout:     post
title:      Store API & createStore的实现
subtitle:   Redux学习笔记系列
date:       2019-05-14
author:     Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
    - Redux
---

## Store API

- getState()
- dispatch(action)
- subscribe(listener)
- replaceReducer(nextReducer)

## `createStore` receives 3 parameters:
```js
createStore(reducer, [preloadedState], [enhancer])
```

## Dive Into Redux
#### wireframe
```js
const createStore = (reducer, preloadedState = {}, middlewares = []) => {
    return {
      getState: () => {...},
      dispatch: (action) => {...},       
      subscribe: (listener) => {...}
    };
}
```

#### Implementation of getState()
```js
let state = initialState;
return {
  getState: () => state,
  ...
}
```


#### Implementation of subscribe()
```js
const listenerFunctionArray = [];
return {
  subscribe: (listener) => {
    listenerFunctionArray.push(listener);
    return () => {
      listenerFunctionArray.splice(listenerFunctionArray.indexOf(listener), 1);}
    }
  },
  ...
}
```

#### Implementation of dispatch()
Basically, `dispatch` is a function that receives an action and triggers state changes to the store
```js
let state = initialState;
const listenerFunctionArray = [];
let dispatchAction = (action) => {
  state = reducer(state, action);
  listenerFunctionArray.forEach(listener => listener());
  return state;
}

...

return {
  dispatch: (action) => dispatchAction(action),
  ...
}
```

In the above implementation we used only the reducer to trigger state changes to the store, but what about our `middlewares`? What about all the `side effects` we want to execute before Redux changes the state?

Before we do that let’s explore the structure of the middleware:
A middleware is a function that returns another function that returns another function, and so on…

Each middleware receives Store's `dispatch` and `getState` functions as named arguments, and returns a function.<br/>
That function will be given the next middleware's dispatch method, and is expected to return a function of action calling next(action) with a potentially different argument, or at a different time, or maybe not calling it at all. <br/>
The last middleware in the chain will receive the real store's dispatch method as the next parameter, thus ending the chain. <br/>
So, the middleware signature is `({ getState, dispatch }) => next => next => ... => next => action`.

```js
let state = initialState;
const listenerArray = [];

let finalMiddleware = (action) => {
  state = reducer(state, action);
  listenerArray.forEach(listener => listener());
  return state;
}

const middlewareAPI = {
  getState: () => state,
  dispatch: (action) => finalMiddleware(action)
}

const newMiddleWareArray = middlewareArray.map(middleware => middleware(middlewareAPI));

//At the end, the finalMiddleware will be the first middleware in the collection, so when we invoke dispatch it will call the first middleware.
for(let i = newMiddleWareArray.length - 1; i >= 0; i--) {
  finalMiddleware = newMiddleWareArray[i](finalMiddleware);
}
```

## Source Code
```js
const createStore = (reducer, initialState = {}, middlewares = []) => {
    let state = initialState;
    const listenerFunctionArray = [];

    // final step - call the reducer and invoke the listenerFunctionArray
    let finalMiddleware = (action) => {
      state = reducer(state, action);
      listenerFunctionArray.forEach(listener => listener());
      return state;
    }

    // the middleware API is constructed of getState and dispatch
    const middlewareAPI = {
        getState: () => state,
        dispatch: (action) => finalMiddleware(action)
    }

    // evalutate the first function in the structure of the middlewares
    const newMiddleWares = middlewares.map(middleware => middleware(middlewareAPI));

    // go over the new middlewares reversed and evaluate the second function in the structure
    // the second function receives the third fucntion of the next middleware
    // this way we can make sure that when the developer will call next(action)
    // he will acually execute the next middleware's most inner funciton
    for(let i = newMiddleWares.length - 1; i >= 0; i--) {
      finalMiddleware = newMiddleWares[i](finalMiddleware);
    }

    return {
      ...middlewareAPI,// getState(), dispatch
      subscribe: (listener) => {
        listenerFunctionArray.push(listener);
        return () => {listenerFunctionArray.splice(listenerFunctionArray.indexOf(listener), 1);}}
    };
}
```



## Example
```js
import { createStore } from 'redux'

function todos(state = [], action) {
  switch (action.type) {
    case 'ADD_TODO':
      return state.concat([action.text])
    default:
      return state
  }
}

const store = createStore(todos, ['Use Redux'])

store.dispatch({
  type: 'ADD_TODO',
  text: 'Read the docs'
})

console.log(store.getState())
// [ 'Use Redux', 'Read the docs' ]
```
