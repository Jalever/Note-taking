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
Data Type: <em>Function</em>

A <strong>reducing function</strong> that returns the next <strong>state tree</strong>, given the <strong>current state tree</strong> and an <strong>action</strong> to handle.

###### preloadedState
Data Type: <em>any</em>

The initial state. You may optionally specify it to hydrate the state from the server in universal apps, or to restore a previously serialized user session. If you produced <strong>reducer</strong> with <strong>combineReducers</strong>, this must be a plain object with the same shape as the keys passed to it. Otherwise, you are free to pass anything that your <strong>reducer</strong> can understand.

###### enhancer
Data Type: <em>Function</em>

The store enhancer. You may optionally specify it to enhance the store with third-party capabilities such as middleware, time travel, persistence, etc. The only store enhancer that ships with Redux is <strong>applyMiddleware()</strong>.

#### Returns
Data Type: <em>Store</em>

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
