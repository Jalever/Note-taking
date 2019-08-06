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
