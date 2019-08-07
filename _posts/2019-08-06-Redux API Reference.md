---
layout: post
title: (Redux)Redux API Reference
subtitle: Getting Started with Redux
date: 2019-08-03
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
---

- [createStore](#createstore)
- [Store](#store)
- [applyMiddleware()](#applyMiddleware)
- [combineReducers(reducers)](#combinereducersreducers)
- [bindActionCreators](#bindactioncreators)
- [compose()](#compose)

## createStore
Creates a Redux store that holds the complete state tree of your app.
> There should only be a single store in your app.

#### Arguments
![eWASw8.png](https://s2.ax1x.com/2019/08/06/eWASw8.png)

###### reducer
Data Type: <ins><em>Function</em></ins>

A <strong>reducing function</strong> that returns the next <strong>state tree</strong>, given the <strong>current state tree</strong> and an <strong>action</strong> to handle.

###### preloadedState
Data Type: <ins><em>any</em></ins>

The initial state. You may optionally specify it to hydrate the state from the server in universal apps, or to restore a previously serialized user session. If you produced <strong>reducer</strong> with <strong>combineReducers</strong>, this must be a plain object with the same shape as the keys passed to it. Otherwise, you are free to pass anything that your <strong>reducer</strong> can understand.

###### enhancer
Data Type: <ins><em>Function</em></ins>

The store enhancer. You may optionally specify it to enhance the store with third-party capabilities such as middleware, time travel, persistence, etc. The only store enhancer that ships with Redux is <strong>applyMiddleware()</strong>.

#### Returns
Data Type: <ins><em>Store</em></ins>

An object that holds the complete state of your app. The only way to change its state is by dispatching actions. You may also subscribe to the changes to its state to update the UI.

#### Example
![eWE72d.png](https://s2.ax1x.com/2019/08/06/eWE72d.png)

#### Tips
- Don't create more than one store in an application! Instead, use <strong>combineReducers</strong> to create a single root reducer out of many.
- It is up to you to choose the state format. You can use plain objects or something like <strong>Immutable</strong>. If you're not sure, start with plain objects.
- If your state is a plain object, make sure you never mutate it! For example, instead of returning something like <strong>Object.assign(state, newData)</strong> from your reducers, return <strong>Object.assign({}, state, newData)</strong>. This way you don't override the previous <strong>state</strong>. You can also write <strong>return { ...state, ...newData }</strong> if you enable the Object Spread Operator proposal.
- For universal apps that run on the server, create a store instance with every request so that they are isolated. Dispatch a few data fetching actions to a store instance and wait for them to complete before rendering the app on the server.
- When a store is created, Redux dispatches a dummy action to your reducer to populate the store with the initial state. You are not meant to handle the dummy action directly. Just remember that your reducer should return some kind of initial state if the state given to it as the first argument is <strong>undefined</strong>, and you're all set.
- To apply multiple store enhancers, you may use <strong>compose()</strong>.

---------------------------------------------------------------------------------------
## Store
A store holds the whole <strong>state tree</strong> of your application. The only way to change the state inside it is to dispatch an <strong>action</strong> on it.

A store is not a class. It's just an object with a few methods on it. To create it, pass your root <strong>reducing function</strong> to <strong>createStore</strong>.

Store Methods
- getState()
- dispatch(action)
- subscribe(listener)
- replaceReducer(nextReducer)

#### getState()
Returns the current state tree of your application. It is equal to the last value returned by the store's reducer.

###### Returns
Data Type: <ins><em>any</em></ins>

The current state tree of your application.

#### dispatch(action)
Dispatches an action. This is the only way to trigger a state change.

The store's reducing function will be called with the current <strong>getState()</strong> result and the given <strong>action</strong> synchronously. Its return value will be considered the next state. It will be returned from <strong>getState()</strong> from now on, and the change listeners will immediately be notified.

###### Arguments
<strong>action</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Data Type: <ins><em>Object</em></ins><br/>
&nbsp;&nbsp;&nbsp;&nbsp;A plain object describing the change that makes sense for your application. Actions are the only way to get data into the store, so any data, whether from the UI events, network callbacks, or other sources such as WebSockets needs to eventually be dispatched as actions. Actions must have a <strong>type</strong> field that indicates the type of action being performed. Types can be defined as constants and imported from another module. It's better to use strings for <strong>type</strong> than Symbols because strings are serializable. Other than <strong>type</strong>, the structure of an action object is really up to you.

###### Returns
Data Type: <ins><em>Object</em></ins>

The dispatched action

###### Notes
The “vanilla” store implementation you get by calling <strong>createStore</strong> only supports plain object actions and hands them immediately to the reducer.

However, if you wrap <strong>createStore</strong> with <strong>applyMiddleware</strong>, the middleware can interpret actions differently, and provide support for dispatching <em>async actions</em>. Async actions are usually asynchronous primitives like Promises, Observables, or thunks.

Middleware is created by the community and does not ship with Redux by default. You need to explicitly install packages like `redux-thunk` or `redux-promise` to use it. You may also create your own middleware.

To learn how to describe asynchronous API calls, read the current state inside action creators, perform side effects, or chain them to execute in a sequence, see the examples for <strong>applyMiddleware</strong>.

###### Example
![eWwy7V.png](https://s2.ax1x.com/2019/08/06/eWwy7V.png)

#### subscribe(listener)
Adds a change listener. It will be called any time an action is dispatched, and some part of the state tree may potentially have changed. You may then call <strong>getState()</strong> to read the current state tree inside the callback.

You may call <strong>dispatch()</strong> from a change listener, with the following caveats:

1. The listener should only call <strong>dispatch()</strong> either in response to user actions or under specific conditions (e. g. dispatching an action when the store has a specific field). Calling <strong>dispatch()</strong> without any conditions is technically possible, however it leads to an infinite loop as every <strong>dispatch()</strong> call usually triggers the listener again.
2. The subscriptions are snapshotted just before every <strong>dispatch()</strong> call. If you subscribe or unsubscribe while the listeners are being invoked, this will not have any effect on the <strong>dispatch()</strong> that is currently in progress. However, the next <strong>dispatch()</strong> call, whether nested or not, will use a more recent snapshot of the subscription list.
3. The listener should not expect to see all state changes, as the state might have been updated multiple times during a nested <strong>dispatch()</strong> before the listener is called. It is, however, guaranteed that all subscribers registered before the <strong>dispatch()</strong> started will be called with the latest state by the time it exits.

To unsubscribe the change listener, invoke the function returned by subscribe.

###### Arguments
<strong>listener</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Data Type: <ins><em>Function</em></ins><br/>
&nbsp;&nbsp;&nbsp;&nbsp;The callback to be invoked any time an action has been dispatched, and the state tree might have changed. You may call <strong>getState()</strong> inside this callback to read the current state tree. It is reasonable to expect that the store's reducer is a pure function, so you may compare references to some deep path in the state tree to learn whether its value has changed.

###### Returns
&nbsp;&nbsp;&nbsp;&nbsp;Data Type: <ins><em>Function</em></ins>

&nbsp;&nbsp;&nbsp;&nbsp;A function that unsubscribes the change listener.

###### Example
![eW6oxU.png](https://s2.ax1x.com/2019/08/06/eW6oxU.png)

#### replaceReducer(nextReducer)
Replaces the reducer currently used by the store to calculate the state.

It is an advanced API. You might need this if your app implements code splitting, and you want to load some of the reducers dynamically. You might also need this if you implement a hot reloading mechanism for Redux.

###### Arguments
<strong>nextReducer</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Data Type: <ins><em>Function</em></ins><br/>

&nbsp;&nbsp;&nbsp;&nbsp;The next reducer for the store to use.

---------------------------------------------------------------------------------------
## applyMiddleware()
Middleware is the suggested way to extend Redux with custom functionality. Middleware lets you wrap the store's <strong>dispatch</strong> method for fun and profit. The key feature of middleware is that it is composable. Multiple middleware can be combined together, where each middleware requires no knowledge of what comes before or after it in the chain.

The most common use case for middleware is to support asynchronous actions without much boilerplate code or a dependency on a library like <strong>Rx</strong>. It does so by letting you dispatch <strong>Async Actions</strong> in addition to normal actions.

For example, <strong>redux-thunk</strong> lets the action creators invert control by dispatching functions. They would receive <strong>dispatch</strong> as an argument and may call it asynchronously. Such functions are called <em><ins>thunks</ins></em>. Another example of middleware is redux-promise. It lets you dispatch a <em>Promise</em> async action, and dispatches a normal action when the Promise resolves.

Middleware is not baked into <strong>createStore</strong> and is not a fundamental part of the Redux architecture, but we consider it useful enough to be supported right in the core. This way, there is a single standard way to extend <strong>dispatch</strong> in the ecosystem, and different middleware may compete in expressiveness and utility.

#### Arguments
![e5K9sO.png](https://s2.ax1x.com/2019/08/07/e5K9sO.png)

###### ...middleware
Data Type: <ins><em>arguments</em></ins><br/>

Functions that conform to the Redux <em>middleware</em> API. Each middleware receives <strong>Store</strong>'s <strong>dispatch</strong> and <strong>getState</strong> functions as named arguments, and returns a function. That function will be given the <strong>next</strong> middleware's dispatch method, and is expected to return a function of <strong>action</strong> calling <strong>next(action)</strong> with a potentially different argument, or at a different time, or maybe not calling it at all. The last middleware in the chain will receive the real store's <strong>dispatch</strong> method as the <strong>next</strong> parameter, thus ending the chain. So, the middleware signature is `({ getState, dispatch }) => next => action`.

###### Returns
Data Type: <ins><em>Function</em></ins><br/>

A store enhancer that applies the given middleware. The store enhancer signature is `createStore => createStore` but the easiest way to apply it is to pass it to <strong>createStore()</strong> as the last <strong>enhancer</strong> argument.

#### Example

###### Custom Logger Middleware
![e5MtNd.png](https://s2.ax1x.com/2019/08/07/e5MtNd.png)
![e5Ma9I.png](https://s2.ax1x.com/2019/08/07/e5Ma9I.png)

###### Using Thunk Middleware for Async Actions
![e5lLX6.png](https://s2.ax1x.com/2019/08/07/e5lLX6.png)
These are the normal action creators you have seen so far.The actions they return can be dispatched without any middleware. However, they only express “facts” and not the “async flow”.
![e51M3n.png](https://s2.ax1x.com/2019/08/07/e51M3n.png)
Even without middleware, you can dispatch an action:
![e51Qcq.png](https://s2.ax1x.com/2019/08/07/e51Qcq.png)

But what do you do when you need to start an asynchronous action, such as an API call, or a router transition?

Meet thunks. A thunk is a function that returns a function. This is a thunk.
![e53kG9.png](https://s2.ax1x.com/2019/08/07/e53kG9.png)

Thunk middleware lets me dispatch thunk async actions as if they were actions!
![e53Ex1.png](https://s2.ax1x.com/2019/08/07/e53Ex1.png)

It even takes care to return the thunk's return value from the dispatch, so I can chain Promises as long as I return them.
![e53er6.png](https://s2.ax1x.com/2019/08/07/e53er6.png)
In fact I can write action creators that dispatch actions and async actions from other action creators, and I can build my control flow with Promises.
![e53YsP.png](https://s2.ax1x.com/2019/08/07/e53YsP.png)
This is very useful for Server Side Rendering, because I can wait until data is available, then synchronously render the app.
![e53LdO.png](https://s2.ax1x.com/2019/08/07/e53LdO.png)
I can also dispatch a thunk async action from a component any time its props change to load the missing data.
![e53vJH.png](https://s2.ax1x.com/2019/08/07/e53vJH.png)

---------------------------------------------------------------------------------------
## combineReducers(reducers)
As your app grows more complex, you'll want to split your <strong>reducing function</strong> into separate functions, each managing independent parts of the <strong>state</strong>.

The <strong>combineReducers</strong> helper function turns an object whose values are different reducing functions into a single reducing function you can pass to <strong>createStore</strong>.

The resulting reducer calls every child reducer, and gathers their results into a single state object. <ins><em>The state produced by <strong>combineReducers()</strong> namespaces the states of each reducer under their keys as passed to <strong>combineReducers()</strong></em></ins>

Example:
![eW4tAg.png](https://s2.ax1x.com/2019/08/06/eW4tAg.png)

You can control state key names by using different keys for the reducers in the passed object. For example, you may call <strong>combineReducers({ todos: myTodosReducer, counter: myCounterReducer })</strong> for the state shape to be <strong>{ todos, counter }</strong>.

A popular convention is to name reducers after the state slices they manage, so you can use ES6 property shorthand notation: <strong>combineReducers({ counter, todos })</strong>. This is equivalent to writing <strong>combineReducers({ counter: counter, todos: todos })</strong>.

#### Arguments
<strong>reducers</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Data Type: <ins><em>Object</em></ins><br/>

&nbsp;&nbsp;&nbsp;&nbsp;An object whose values correspond to different reducing functions that need to be combined into one. See the notes below for some rules every passed reducer must follow.

#### Returns
&nbsp;&nbsp;&nbsp;&nbsp;Data Type: <ins><em>Function</em></ins><br/>

&nbsp;&nbsp;&nbsp;&nbsp;A reducer that invokes every reducer inside the <strong>reducers</strong> object, and constructs a state object with the same shape.

#### Notes
This function is mildly opinionated and is skewed towards helping beginners avoid common pitfalls. This is why it attempts to enforce some rules that you don't have to follow if you write the root reducer manually.

Any reducer passed to <strong>combineReducers</strong> must satisfy these rules:
- For any action that is not recognized, it must return the <strong>state</strong> given to it as the first argument.
- It must never return <strong>undefined</strong>. It is too easy to do this by mistake via an early <strong>return</strong> statement, so <strong>combineReducers</strong> throws if you do that instead of letting the error manifest itself somewhere else.
- If the <strong>state</strong> given to it is <strong>undefined</strong>, it must return the initial state for this specific reducer. According to the previous rule, the initial state must not be <strong>undefined</strong> either. It is handy to specify it with ES6 optional arguments syntax, but you can also explicitly check the first argument for being <strong>undefined</strong>.

While <strong>combineReducers</strong> attempts to check that your reducers conform to some of these rules, you should remember them, and do your best to follow them. <strong>combineReducers</strong> will check your reducers by passing <strong>undefined</strong> to them; this is done even if you specify initial state to <strong>Redux.createStore(combineReducers(...), initialState)</strong>. Therefore, you must ensure your reducers work properly when receiving <strong>undefined</strong> as state, even if you never intend for them to actually receive <strong>undefined</strong> in your own code.

#### Example
![eWIskF.png](https://s2.ax1x.com/2019/08/06/eWIskF.png)
![eWIyY4.png](https://s2.ax1x.com/2019/08/06/eWIyY4.png)
![eWo4vn.png](https://s2.ax1x.com/2019/08/06/eWo4vn.png)
![eWoX8J.png](https://s2.ax1x.com/2019/08/06/eWoX8J.png)

---------------------------------------------------------------------------------------
## bindActionCreators()
Turns an object whose values are Action Creators, into an object with the same keys, but with every action creator wrapped into a <strong>Dispatch</strong> call so they may be invoked directly.

Normally you should just call <strong>dispatch</strong> directly on your <strong>Store</strong> instance. If you use Redux with React, <strong>react-redux</strong> will provide you with the <strong>dispatch</strong> function so you can call it directly, too.

The only use case for <strong>bindActionCreators</strong> is when you want to pass some action creators down to a component that isn't aware of Redux, and you don't want to pass <strong>dispatch</strong> or the Redux store to it.

For convenience, you can also pass an action creator as the first argument, and get a dispatch wrapped function in return.

#### Parameters
![e5iW1H.png](https://s2.ax1x.com/2019/08/07/e5iW1H.png)

###### actionCreators
Data Type: <ins><em>Function or Object</em></ins>

An <strong>action creator</strong>, or an <strong>object</strong> whose values are action creators.

###### dispatch
Data Type: <ins><em>Function</em></ins>

A dispatch function available on the Store instance.

#### Parameters
###### actionCreators
Data Type: <ins><em>Function or Object</em></ins>

An <strong>action creator</strong>, or an <strong>object</strong> whose values are action creators.

###### dispatch
Data Type: <ins><em>Function</em></ins>

A dispatch function available on the Store instance.

#### Returns
Data Type: <ins><em>Function or Object</em></ins>

An object mimicking the original object, but with each function immediately dispatching the action returned by the corresponding action creator. If you passed a function as <strong>actionCreators</strong>, the return value will also be a single function.

#### Example
![e5Ccb6.png](https://s2.ax1x.com/2019/08/07/e5Ccb6.png)
![e5PKqx.png](https://s2.ax1x.com/2019/08/07/e5PKqx.png)
![e5PNQA.png](https://s2.ax1x.com/2019/08/07/e5PNQA.png)
![e5Pfe0.png](https://s2.ax1x.com/2019/08/07/e5Pfe0.png)
![e5PzFO.png](https://s2.ax1x.com/2019/08/07/e5PzFO.png)
![e5is76.png](https://s2.ax1x.com/2019/08/07/e5is76.png)

---------------------------------------------------------------------------------------
## compose()
Composes functions from right to left.

This is a functional programming utility, and is included in Redux as a convenience.
You might want to use it to apply several Store Enhancers in a row.

#### Arguments
![e5XVpt.png](https://s2.ax1x.com/2019/08/07/e5XVpt.png)

Data Type: <ins><em>arguments</em></ins>

The functions to compose. Each function is expected to accept a single parameter. Its return value will be provided as an argument to the function standing to the left, and so on. The exception is the right-most argument which can accept multiple parameters, as it will provide the signature for the resulting composed function.

#### Returns
Data Type: <ins><em>Function</em></ins>

The final function obtained by composing the given functions from right to left.

#### Example
This example demonstrates how to use <strong>compose</strong> to enhance a <strong>store</strong> with <strong>applyMiddleware</strong> and a few developer tools from the <strong>redux-devtools</strong> package.
![e5jrVg.png](https://s2.ax1x.com/2019/08/07/e5jrVg.png)

#### Tips
All <strong>compose</strong> does is let you write deeply nested function transformations without the rightward drift of the code. Don't give it too much credit!
